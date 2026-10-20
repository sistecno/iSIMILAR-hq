> ⚠️ Texto copiado íntegro del antiguo CLAUDE.md (oct 2026). Algunas partes están desactualizadas (créditos, versiones, dimensiones, tiempos). Ante cualquier duda manda el código; resumen vigente en `../iSIMILAR-hq/docs/definicion-tecnica.md`.


## 5. Pipeline de Escaneo

### Flujo completo

```
photo_manager.thumbnailDataWithSize(ThumbnailSize(224, 224), quality: 80)
        ↓
Dart Isolate nativo (NO usar flutter_isolate)
        ↓
tflite_flutter + GPU/CoreML delegate
        ↓  ~4-5ms por foto
Vector float32[576]
        ↓
ObjectBox putMany() cada 50 fotos (escritura transaccional)
        ↓
Checkpoint: guardar último assetId procesado en ConfigEntity
```

### Código del Isolate (pseudocódigo de referencia)

```dart
Future<void> scannerWorker(SendPort sendPort) async {
  // 1. Abrir ObjectBox y cargar TFLite EN EL ISOLATE (no en main thread)
  final store = openStore();
  final interpreter = await Interpreter.fromAsset(
    'assets/mobilenet_v3_small_feature_uint8.tflite',
    options: interpreterOptions, // con GPU/CoreML delegate
  );

  // 2. Deduplicación eficiente — cargar IDs existentes en Set ANTES del loop
  final existingIds = store.box<ImagenEntity>()
      .getAll()
      .map((e) => e.assetId)
      .toSet(); // O(1) lookup, no O(n) queries

  // 3. Loop de procesamiento
  List<ImagenEntity> batch = [];
  int processedCount = 0;

  for (var asset in assets) {
    if (existingIds.contains(asset.id)) continue; // skip ya procesadas

    final thumb = await asset.thumbnailDataWithSize(ThumbnailSize(224, 224));
    if (thumb == null) continue;

    // Inferencia
    final embedding = runInference(interpreter, thumb); // → List<double>[576]

    batch.add(ImagenEntity(
      assetId: asset.id,
      timestamp: asset.createDateTime.millisecondsSinceEpoch,
      scannedAt: DateTime.now().millisecondsSinceEpoch,
      embedding: embedding,
    ));

    processedCount++;

    // Escritura por lotes — nunca put() individual dentro del loop
    if (batch.length >= 50) {
      store.box<ImagenEntity>().putMany(batch);
      batch.clear();
      // Guardar checkpoint
      saveCheckpoint(store, asset.id);
    }

    // Throttle de UI — no enviar mensaje por cada foto (satura Event Loop)
    if (processedCount % 100 == 0) {
      sendPort.send(processedCount);
    }
  }

  // Guardar remanentes
  if (batch.isNotEmpty) store.box<ImagenEntity>().putMany(batch);
  interpreter.close();
  store.close();
}
```

### Escaneo incremental (aperturas posteriores)

```
Al abrir la app (después del primer escaneo):
1. Leer scannedAt más reciente en ObjectBox
2. photo_manager.getAssetListRange() filtrando por fecha > scannedAt
3. Solo procesar fotos nuevas
4. Si 0 fotos nuevas → instantáneo, sin indicador de progreso
```

---

## 6. Estrategia de Escaneo por Plataforma

### Android

```
DEFAULT ON (incluidas automáticamente):
├── Camera (DCIM/Camera)
├── Screenshots
├── Pictures
└── Downloads

DEFAULT OFF (el usuario activa):
├── WhatsApp    → texto: "Incluir para encontrar memes e imágenes similares"
├── Telegram    → ídem
└── Instagram   → ídem

UI onboarding: mostrar lista de álbumes con nombre + conteo de fotos + estimado de tiempo
Android 14: detectar acceso parcial → banner "Acceso limitado" + botón para ampliar
Paginación: 500 assets por batch para no saturar memoria
```

### iOS

```
DEFAULT ON:
└── Recientes (toda la biblioteca — comportamiento esperado en iOS)

DEFAULT OFF (el usuario excluye):
├── WhatsApp    → texto: "Excluir mensajería para un escaneo más limpio"
├── Telegram    → ídem
└── Otros álbumes de apps

iCloud Photos: usar SIEMPRE thumbnails, nunca originFile
               El thumbnail es local aunque la foto esté en iCloud
HEIC / Live Photos: photo_manager los maneja transparentemente
iOS 14+: detectar PHAuthorizationStatusLimited → banner informativo
```

### Estimado de tiempo (mostrar antes de confirmar escaneo)

```
Calcular en base a fotos seleccionadas:
[X] Camera:     2.341 fotos
[X] Screenshots:  892 fotos
[ ] WhatsApp:   8.432 fotos  (no incluido)
──────────────────────────────
Total a escanear: 3.233 fotos
Tiempo estimado:  ~30 segundos
```

---

## 7. Búsqueda de Similares

```
1. Usuario selecciona imagen base
2. Generar embedding de la imagen base en Isolate (~5ms)
3. ObjectBox HNSW query:
   box.query(ImagenEntity_.embedding.nearestNeighborsF32(queryVector, 50))
4. Retorna top 50 resultados ordenados por similitud (coseno aproximado)
5. UI muestra resultados como "Relacionados" (NO mostrar porcentaje)
   Tiempo total: < 50ms para cualquier tamaño de galería
```

---

## 8. Feature "Buscar Memes"

```
Implementación Phase 1:
- Bundled en assets/meme_references/ → 5-8 imágenes de referencia
  que representan formatos visuales comunes de memes
- Al tocar "Buscar Memes":
  1. Generar embeddings de las referencias internas
  2. Para cada referencia, buscar top-50 similares
  3. Combinar y deduplicar resultados
  4. Mostrar: "Encontramos ~340 imágenes similares a memes"
- Si carpetas de mensajería no están incluidas → banner para activarlas

Implementación Phase 2 (clustering):
- DBSCAN sobre embeddings de carpetas de mensajería
- Sin imagen base, agrupa por similitud automáticamente
- Muestra grupos: "47 imágenes similares", "23 imágenes similares", etc.
```

---

## 9. Acciones Post-Búsqueda (universales)

Las mismas acciones aplican para búsqueda normal y Buscar Memes:

```
GRATIS (siempre disponible):
├── Ver resultados
├── Seleccionar imágenes individualmente
├── Borrar una por una (tedioso — incentivo a comprar créditos)
└── Compartir selección

CON CRÉDITO (1 crédito = 1 acción en lote):
├── Borrar N imágenes seleccionadas
├── Mover selección a álbum (existente o nuevo)
└── Exportar selección

TRIAL: 5 acciones en lote gratuitas al instalar la app
```

### iOS — Regla crítica de créditos

```
El crédito se descuenta SOLO DESPUÉS de que photo_manager
confirma que la eliminación fue exitosa.
Si el usuario rechaza el popup del sistema → NO descontar crédito.
```
