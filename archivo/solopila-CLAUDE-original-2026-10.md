# Solopila — Guía de Arquitectura y Desarrollo

> Documento de referencia para Claude y el equipo de desarrollo.
> Toda decisión arquitectural aquí registrada fue discutida y aprobada.
> Última actualización: Febrero 2026

---

## 0. Reglas de Colaboración con Claude

### Ante ideas nuevas
Cuando el usuario presente una idea nueva, Claude DEBE:
1. Registrarla en este archivo (CLAUDE.md) al principio, en esta sección.
2. Cuestionar la idea con lógica — pros, contras, riesgos reales.
3. Destruir los argumentos débiles con evidencia o razonamiento, sin importar quién los proponga.
4. Hacer preguntas serias y verificables con el objetivo de encontrar el plan óptimo, no de validar la idea original.

### Modo de respuesta
- **No seguir la corriente.** Si una idea tiene un fallo, decirlo directamente.
- **Decir lo que se necesita escuchar, no lo que se quiere escuchar.**
- **Contradecir y criticar cuando corresponda** — sin miedo, sin suavizar.
- **Cero sesgo de complacencia** hacia el usuario.
- El objetivo es el mejor resultado posible para el producto, no la aprobación del usuario.

### Idea registrada (Feb 2026): Destilación DINOv2 → MobileNetV3
Estado: EN EJECUCIÓN bajo control de Claude. Feedback crítico aplicado; ver sección 17.
Decisiones cerradas:
1. Se entrena directamente (sin F2 bloqueante), con Claude controlando cada artefacto.
2. Normalización ImageNet horneada en el grafo TFLite → la app sigue enviando 0–255 crudo.
3. Dataset de entrenamiento mixto: base genérica + refuerzo de categorías del producto.
4. Anti-fuga obligatorio: limpieza automática de solapamiento train/eval antes de entrenar.
Detail operativo y puntos de control: sección 17.

### Idea registrada (Oct 2026): Telemetría de producto (RevenueCat + Firebase Analytics)
Estado: IMPLEMENTADO (medición). Pendiente: limpieza de créditos en versión aparte.

Objetivo: entender el embudo real — cuántos terminan el escaneo, cuántos llegan a una
acción en lote y qué segmento paga.

Atributos de RevenueCat (`Purchases.setAttributes`, vía `AnalyticsService`):
1. `paywall_trigger` → `camera` · `batch_delete` · `batch_album` · `settings`.
2. `batch_size` → nº de fotos seleccionadas al abrir el muro (solo cuando aplica).
3. `gallery_size` → `<3k` · `3-10k` · `>10k` (una vez: tras el escaneo o al
   arrancar si el usuario ya tenía fotos escaneadas).
4. `use_case` → `work_repair` · `work_field` · `work_creative` · `work_other` ·
   `memes_screenshots` · `everyday_photos` · `other`.

Eventos de Firebase Analytics:
`scan_started` {photo_count} · `scan_completed` {photo_count, duration_seconds} ·
`search_gallery` · `search_camera` · `photo_action` {action, photo_count, is_batch,
paywall_shown} · `paywall_shown` {trigger}.

Decisiones cerradas:
1. El evento de acciones se llama `photo_action` (no `batch_attempt`): incluye acciones
   individuales y de lote; `is_batch` distingue. `action`: `delete`, `move_album`,
   `remove_album`, `share`.
2. "Quitar de álbum" es `remove_album`, NO `move_album` (acciones distintas).
3. El valor guardado NUNCA se traduce; solo cambia el texto visible por idioma.
4. `use_case`: se pregunta una sola vez tras un cierre con éxito del muro (compra o
   inicio de prueba), nunca en "Restaurar compras", siempre con opción de omitir.
   `purchases_flutter` no expone lectura de atributos → control con flag local
   (SharedPreferences). NUNCA embeber la clave secreta de RevenueCat.
5. Privacidad (coherente con la etiqueta App Store, sin "tracking"): sin IDFA en iOS
   (`$FirebaseAnalyticsWithoutAdIdSupport`), sin Advertising ID en Android
   (`google_analytics_adid_collection_enabled=false` + `AD_ID` con `tools:node="remove"`)
   y Consent Mode con señales de publicidad denegadas (`AnalyticsService.init`).
6. La limpieza del sistema de créditos (modelo `CreditEntity`, strings y textos) va en
   OTRA versión: toca el schema de ObjectBox. Solo se renombró el botón de Ajustes
   (`get_credits` → `go_pro`, "Mejora a iSIMILAR PRO").

---

## 1. Concepto Central de la App

**Solopila** es un motor de búsqueda visual universal para galerías de fotos.

### Función principal
El usuario selecciona UNA imagen como referencia (base) y la app encuentra
todas las imágenes visualmente similares dentro de su galería.

### Regla de oro
> Siempre existe una imagen base. La app nunca genera grupos
> de similares "solos". Todo parte de una imagen de referencia elegida
> por el usuario o por la app (en features especiales como Buscar Memes).

### Casos de uso validados
- Técnico de PC: foto de una placa base → encuentra todas sus fotos de placas
- Arquitecto: foto de construcción → encuentra similares de obra
- Médico: radiografía → encuentra las 1500 radiografías de su galería
- Fotógrafo: foto de playa → encuentra todas las fotos de playa
- Cualquier usuario: cualquier foto → similares en su galería personal

### Lo que NO es esta app
- NO es un buscador de duplicados exactos
- NO es un organizador automático sin intervención del usuario
- NO es exclusiva para memes (los memes son una feature adicional)

---

## 2. Stack Tecnológico Definitivo

### Dependencias (pubspec.yaml)

```yaml
dependencies:
  # Galería — acceso nativo a thumbnails del OS
  photo_manager: ^3.2.2               # ya existe en el proyecto

  # IA — motor de inferencia con acceso GPU/NPU
  tflite_flutter: ^0.10.4             # NUEVO

  # Base de datos vectorial con índice HNSW
  objectbox: ^4.0.0                   # NUEVO — reemplaza sqflite
  objectbox_flutter_libs: ^4.0.0      # NUEVO

  # Monetización
  purchases_flutter: ^8.0.0           # NUEVO — RevenueCat

  # Notificaciones push + control de versiones
  firebase_core: ^3.0.0               # NUEVO — requerido por Firebase
  firebase_messaging: ^15.0.0         # NUEVO — push notifications
  firebase_remote_config: ^5.0.0      # NUEVO — actualizaciones forzadas (min_build_number)
  firebase_crashlytics: ^4.0.0        # NUEVO — errores en Isolate
  package_info_plus: ^8.0.0           # NUEVO — leer build number en runtime

  # Procesamiento de imagen (redimensionar si necesario)
  image: ^4.3.0                       # ya existe en el proyecto

dev_dependencies:
  objectbox_generator: ^4.0.0         # NUEVO — genera código ObjectBox
```

> ADVERTENCIA: ObjectBox HNSW (búsqueda vectorial) solo existe desde v4.0.0.
> No usar versiones anteriores (2.x o 3.x).

---

## 3. Modelo de IA

### Especificaciones del modelo

```
Arquitectura:  MobileNetV3-Small — HEADLESS (feature extractor)
               NO usar el modelo de clasificación (da 1001 clases, inútil)
               USAR el "feature_vector" que da el embedding real

Fuente:        TF Hub → mobilenet_v3_small_100_224/feature_vector
Archivo:       assets/mobilenet_v3_small_feature_uint8.tflite

Input:         224 × 224 px — uint8 (0-255, sin normalización en Dart)
               IMPORTANTE: buscar modelo que acepte uint8 directo
               Evitar el modelo float32 input (requiere conversión costosa en Dart)

Output:        576 dimensiones — float32
               Este es el embedding visual de la imagen

Tamaño:        ~3MB
Latencia:      ~4ms Android (GPU) / ~3-5ms iOS (Neural Engine)
```

### Aceleración por hardware (OBLIGATORIA)

```dart
// Android — GpuDelegateV2
final gpuDelegate = GpuDelegateV2(
  options: GpuDelegateOptionsV2(
    isPrecisionLossAllowed: true,
    inferencePreference: TfLiteGpuInferenceUsage.fastSingleAnswer,
  ),
);

// iOS — CoreMlDelegate
final coremlDelegate = CoreMlDelegate();

// Uso:
var options = InterpreterOptions();
if (Platform.isAndroid) options.addDelegate(gpuDelegate);
if (Platform.isIOS) options.addDelegate(coremlDelegate);
```

> Sin GPU/CoreML delegate la latencia sube 4x. Es obligatorio en producción.

---

## 4. Base de Datos — ObjectBox

### Entidad principal

```dart
@Entity()
class ImagenEntity {
  @Id()
  int id = 0;

  @Index()
  String assetId;         // ID único del asset en la galería del OS

  int timestamp;          // fecha de creación — Unix ms (para hybrid score futuro)
  int scannedAt;          // cuándo fue procesada — Unix ms (checkpoint de escaneo)
  bool isInAlbum;         // gestión de álbumes

  // Vector visual — índice HNSW para búsqueda de vecinos más cercanos
  @HnswIndex(dimensions: 576)
  List<double>? embedding;

  // Metadata futura (Phase 3)
  // double? latitude;
  // double? longitude;
}
```

### Entidad de configuración

```dart
@Entity()
class ConfigEntity {
  @Id()
  int id = 0;
  String key;
  String value;
}
// Almacena: carpetas seleccionadas, último assetId escaneado, preferencias UI
```

### Entidad de créditos

```dart
@Entity()
class CreditEntity {
  @Id()
  int id = 0;
  int balance;            // saldo actual de créditos
  int lastUpdated;        // Unix ms
}
```

### Migración desde SQLite

La app actual usa SQLite v3 con tablas `images` y `labels`.
Al actualizar, la migración es silenciosa y automática:
1. Al arrancar, detectar si existe DB SQLite
2. Si existe: borrar SQLite silenciosamente, iniciar ObjectBox limpio
3. Iniciar escaneo completo automáticamente
4. No mostrar ningún modal ni pedir confirmación al usuario
   (la app tiene pocos usuarios — migración transparente es lo correcto)

---

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

---

## 10. Monetización

### Modelo: Créditos + Suscripción anual + Trial de 7 días

```
PACKS DE CRÉDITOS (consumable IAP):
├── Starter:   10 créditos → $1.99
├── Pro:       50 créditos → $4.99
└── Mega:     150 créditos → $9.99

SUSCRIPCIÓN (usuarios frecuentes):
└── Anual: $19.99/año → acciones en lote ilimitadas
    └── TRIAL: 7 días gratis (introductorio) — Implementado Abr 2026

TIER GRATUITO:
├── Escanear galería completa          ✅
├── Buscar similares                   ✅
├── Ver resultados                     ✅
├── 5 búsquedas con cámara (local)     ✅
└── Borrar una por una                 ✅ siempre
```

### Implementación del Trial de 7 días (Abril 2026)

- **Configuración Nativa**: Configurado como "Introductory Offer" en App Store Connect y como "Oferta de Adquisición" en Google Play Console.
- **Detección Dinámica**: `PremiumService` detecta si el producto anual tiene un `introductoryPrice` con coste 0.
- **UI de Conversión**:
  - `PremiumOfferSheet`: El botón principal cambia dinámicamente a "Start 7-Day Free Trial".
  - `CreditsHero`: Se añadió un badge de trial ("⭐ 7 DAYS FREE") para incentivar la conversión desde Ajustes.

### Protocolo de Verificación Técnica (Play Store / App Store)

Para evitar conjeturas al implementar trials en otras apps, seguir este checklist:

1.  **Detección de Oferta**: Inyectar log en el servicio para confirmar que la tienda envía la oferta:
    `print("DEBUG: ${product.identifier} - Intro: ${product.introductoryPrice?.price}");`
2.  **Elegibilidad de Tester**: 
    - **iOS**: Resetear "Introductory Eligibility" en los ajustes de la cuenta Sandbox del dispositivo.
    - **Android**: Google Play es estricto. Si la cuenta ya usó un trial, NO lo mostrará. **Obligatorio** probar con una cuenta de Gmail "virgen" (nueva) y en modo `--profile` para ver logs.
3.  **Confirmación de Tienda**: Al iniciar la compra, el diálogo nativo (System Sheet) DEBE decir explícitamente: *"Gratis por 7 días"* o *"No se te cobrará nada hasta el [Fecha]"*. Si esto no aparece, el trial no está activo en la tienda aunque el badge de la app lo diga.
4.  **Dashboard Sync**: En RevenueCat, el producto debe mostrar "Introductory Price: Free trial" o "$0.00" tras sincronizar las credenciales de la tienda.


### Implementación con RevenueCat

- SDK: `purchases_flutter`
- Créditos = consumable IAP
- Suscripción anual = auto-renewable subscription
- RevenueCat valida compras con App Store / Google Play
- Saldo de créditos guardado localmente en `CreditEntity` (ObjectBox)
- NO construir backend de pagos propio

---

## 11. Arquitectura de Datos

```
LOCAL (dispositivo):
├── ObjectBox
│   ├── ImagenEntity     → embeddings + metadata de fotos (NO imágenes)
│   ├── ConfigEntity     → carpetas seleccionadas, checkpoint, prefs
│   └── CreditEntity     → saldo de créditos
│
└── Almacenamiento: ~2.3KB por foto (solo vector + metadata)
    10.000 fotos = ~23MB total en DB
    Las imágenes originales NUNCA se tocan, copian ni mueven.
    La UI las referencia por assetId desde su ubicación natural.

EXTERNO (sin backend propio en Phase 1):
├── RevenueCat Cloud     → historial de transacciones, entitlements
├── Firebase FCM         → notificaciones push para anuncios y updates
└── App Store / Google   → procesamiento de pagos
```

---

## 11b. Notificaciones y Comunicación con el Usuario

### Recordatorios automáticos — Notificaciones locales
```
Paquete: flutter_local_notifications (ya existe en el proyecto)
Sin backend, sin servidor, funciona offline.

Casos de uso:
├── Recordatorio post-escaneo: programar notificación 30 días después
│   "Han pasado 30 días. Tu galería puede tener fotos nuevas."
└── Recordatorio semanal: configurable en Settings (ON/OFF por el usuario)
```

### Anuncios y actualizaciones — Firebase Cloud Messaging
```
Paquetes nuevos:
├── firebase_core: ^3.x.x
└── firebase_messaging: ^15.x.x

Flujo:
App instala → registra token FCM → guardado en Firebase
Tú (desarrollador) → Firebase Console → redactas mensaje → envías a todos

No requiere backend propio.
Firebase Console es la interfaz de envío para:
├── "Nueva versión disponible con búsqueda por texto"
├── Promociones de créditos
└── Recordatorios de temporada
```

---

## 11c. Actualizaciones Forzadas — Firebase Remote Config

### Por qué es necesario
Cuando publiques una versión con cambios al schema de ObjectBox, una nueva
lógica de negocio crítica, o un fix de seguridad, necesitas que los usuarios
en versiones viejas sean forzados a actualizar. Sin este mecanismo, usuarios
con la versión 1.0.0+4 seguirán usando la app aunque hayas publicado la 1.0.0+9.

### Implementación
```
Paquetes:
├── firebase_remote_config: ^5.x.x   → almacena min_build_number
└── package_info_plus: ^8.x.x        → lee el build number actual en runtime

Flujo al arrancar la app (antes de runApp o en splash):
1. Fetch Remote Config → min_build_number (int, ej: 5)
2. PackageInfo.fromPlatform() → buildNumber (ej: "4")
3. Si int.parse(buildNumber) < min_build_number:
   → Dialog NO dismissible:
     "Hay una actualización importante disponible"
     "Esta versión ya no está soportada. Por favor actualiza para continuar."
     [Actualizar ahora] → url_launcher abre App Store / Play Store
4. Si versión OK → continuar normalmente

Remote Config key: min_build_number (tipo Number, default: 1)
```

### Reglas
```
❌ NUNCA bloquear si Remote Config falla (timeout/sin internet)
   → Si falla el fetch, dejar pasar al usuario normalmente
✅ Timeout del fetch: 10 segundos máximo
✅ Activar inmediatamente después de fetch (fetchAndActivate)
✅ Default value en el código: min_build_number = 1 (nunca bloquea por defecto)
```

### URLs de tienda
```dart
const appStoreUrl = 'https://apps.apple.com/app/id[APP_ID]';
const playStoreUrl = 'https://play.google.com/store/apps/details?id=com.solopila.app';
```

---

## 12. Lo que Cambia vs Código Actual

### Eliminar
- `ImageClassificationService` (ML Kit labels)
- Tabla SQLite `labels`
- Tabla SQLite `images`
- Dependencia `sqflite`
- Dependencia `google_mlkit_image_labeling`

### Reemplazar
- `DatabaseService` (SQLite) → `ObjectBoxService`
- `ImageModel.similarityWith()` (dot product en labels) → HNSW query

### Crear
- `EmbeddingService` (TFLite + GPU/CoreML)
- `ScanIsolateService` (worker con checkpoint + incremental)
- `VectorSearchService` (wrapper de HNSW query ObjectBox)
- `CreditService` (saldo local + validación RevenueCat)

### Mantener intacto
- Toda la UI (home_view, image_selection_view, settings, progress, widgets)
- `HomeViewModel` estructura general
- `photo_manager` integration (ajustar thumbnail de 256→224px)
- `ThumbnailManagerService` (ajuste mínimo de tamaño)
- Sistema de álbumes
- Localization EN/ES/IT
- `FileManagementService`
- Permisos y ciclo de vida

---

## 13. Fases de Desarrollo

### Phase 1 — Core + Monetización (prioridad)
```
Bloque A: Core técnico
├── EmbeddingService (TFLite + GPU/CoreML)
├── ObjectBox schema v4 + migración desde SQLite v3
├── ScanIsolateService (checkpoint + incremental + throttle)
└── VectorSearchService (HNSW query)

Bloque B: Monetización (simultáneo)
├── RevenueCat setup (productos en App Store Connect + Play Console)
├── CreditService
├── Shop UI
└── Paywall en batch actions (con regla iOS: crédito post-confirmación)

Bloque C: Estabilidad + Comunicación
├── Bug ProgressView "0/0" flash en aperturas sin fotos nuevas
├── Firebase setup (core + messaging + remote_config + crashlytics)
├── Actualizaciones forzadas (Remote Config min_build_number)
├── Notificaciones locales (recordatorio 30 días — flutter_local_notifications)
├── Push notifications FCM (anuncios y promos — Firebase Console)
└── Crashlytics en Isolate (try-catch en _workerEntry)
```

### Phase 2 — Features diferenciadoras
```
├── CLIP-Lite: búsqueda por texto (Premium exclusivo)
│   Ejemplo: usuario escribe "radiografía" → encuentra todas
└── Buscar Memes v2: clustering DBSCAN automático
```

### Phase 3 — Escalabilidad y precisión
```
├── Hybrid scoring: 80% visual + 10% fecha + 10% GPS
└── Evaluación de migración a backend si se necesita sync cross-device
```

---

## 14. Métricas de Rendimiento Esperadas

```
Escaneo primer uso:
├── 1.000 fotos  →  ~10 segundos
├── 5.000 fotos  →  ~50 segundos
└── 15.000 fotos →  ~2.5 minutos

Búsqueda de similares:
└── < 50ms sin importar el tamaño de la galería (HNSW)

Almacenamiento en DB:
├── 576 dims × 4 bytes = ~2.3KB por foto
└── 10.000 fotos = ~23MB total

Tamaño del modelo en el app:
└── ~3MB (bundled en assets)
```

---

## 15. Errores Críticos a Evitar

```
❌ Usar objectbox < 4.0.0 — HNSW no existe en versiones anteriores
❌ Usar el modelo de clasificación (1001 outputs) — necesitas el headless
❌ Input float32 al modelo — buscar modelo que acepte uint8 para evitar conversión
❌ Usar flutter_isolate — usar Dart Isolate nativo
❌ put() individual en loop — siempre putMany() cada 50 items
❌ Enviar SendPort message por cada foto — throttle cada 100 fotos
❌ Descontar crédito antes de confirmación iOS — siempre post-éxito
❌ Query ObjectBox por foto dentro del loop — cargar Set de IDs antes del loop
❌ Leer asset.originFile durante escaneo — solo thumbnails
❌ GpuDelegateV2 en iOS — usar CoreMlDelegate
❌ CoreMlDelegate en Android — usar GpuDelegateV2
```

---

## 16. Notas de UX Aprobadas

```
✅ Mostrar "Relacionados" — NO mostrar porcentaje de similitud
✅ 5 acciones de lote gratuitas como trial real (no castigo)
✅ El usuario puede siempre borrar una por una (gratis y tedioso)
✅ Estimado de tiempo antes de confirmar escaneo
✅ Escaneo no bloquea UI — el usuario puede usar la app mientras indexa
✅ Texto carpetas mensajería: "Incluir para encontrar memes e imágenes similares"
✅ Migración SQLite → ObjectBox: silenciosa y automática, sin modal
✅ Progress indicator discreto durante indexación ("Analizando... 234/1500")
```


## Pre-lanzamiento — Checklist
[x] Botón "Restaurar Compras" — implementado en PremiumOfferSheet footer.
[x] Privacy Policy URL en la ficha de la tienda — configurado.
[x] Permiso NSPhotoLibraryUsageDescription en Info.plist — configurado.
[x] Manejo de permisos Android 13 (READ_MEDIA_IMAGES) vs Android <13 — resuelto.
[x] Crashlytics configurado para capturar errores dentro del Isolate — resuelto.
[x] Actualizaciones forzadas configuradas (Firebase Remote Config min_build_number) — activo.
[x] App Store ID obtenido y URLs de tienda definidas — app publicada en ambas tiendas.

## Pendiente técnico (post-release)
[ ] Eliminar CreditEntity del schema ObjectBox (credit_entity.dart + regenerar objectbox.g.dart).
[ ] Actualizar Firebase Remote Config min_build_number a 15 tras publicar versión 1.1.0+15.

## Android 15 — Pendiente próxima versión
Advertencias de Play Store (no bloquean, pero hay que resolverlas):

**1. Edge-to-edge obligatorio (SDK 35)**
Android 15 muestra apps de extremo a extremo por defecto. Hay que gestionar insets.
Fix en Flutter: revisar `SystemChrome` o llamar `enableEdgeToEdge()` en `MainActivity.kt`.

**2. APIs deprecadas en Android 15**
Play Console detectó uso de:
- `Window.setStatusBarColor`
- `Window.setNavigationBarColor`
- `Window.setNavigationBarDividerColor`

Origen: engine interno de Flutter (`io.flutter.plugin.platform`), no código propio.
Fix: actualizar Flutter SDK a versión reciente (probablemente ya resuelto en Flutter 3.x reciente).

---

## 17. Destilación DINOv2 → MobileNetV3 (Roadmap operativo)

> Idea registrada Feb 2026. Estado: en ejecución bajo control de Claude.
> Reemplaza la propuesta inicial, que asumía MobileNetV3-Small/576 y partía de cero.
> Baseline real: `isimilar_mobilenetv3_large_v1` — MobileNetV3-Large, **960 dims**,
> **mAP 0.790** sobre las 917 imágenes de `tools/similarity_eval`.

### 17.1 Decisiones cerradas
1. Se entrena directamente; Claude controla cada artefacto antes de avanzar de fase.
2. Normalización ImageNet **horneada dentro del grafo TFLite** → la app sigue
   alimentando float32 crudo 0–255 (igual que hoy). El modelo es drop-in real.
3. Dataset de entrenamiento **mixto**: base genérica + sobrerrepresentación de las
   categorías del producto (boards, baterias, circuitos, pantallas, documentos, memes).
4. **Sin fuga de datos**: limpieza automática de solapamiento train/eval antes de entrenar.

### 17.2 Pipeline con puntos de control
```
F0.5  Preparación y anti-fuga            (Claude)
F1    Calibración del modelo actual      (ya existe, harness)
F2    Referencia superior DINOv2         (no bloqueante; recomendado)
F3    Pre-cálculo de targets             (Claude valida)
F4    Entrenamiento del student          (usuario ejecuta, Claude revisa)
F5    Export a TFLite FP16               (Claude valida)
F6    Gate de calidad obligatorio         (Claude)
F7    Integración Flutter + migración    (Claude)
```

- **F0.5 — Preparación y anti-fuga (Claude):**
  Inventario con SHA-256 exacto + perceptual hash (near-duplicates). Eliminar del
  train cualquier imagen que colisione con el set de eval 917. Salida:
  `manifest.json` (rutas ordenadas = índice de los targets), conteos y reporte de
  duplicados. Gate: 0 colisiones exactas y revisión manual de near-dups.
- **F2 — Referencia superior:** DINOv2-S sobre el heldout sólo como techo de
  referencia; no bloquea el entrenamiento.
- **F3 — Targets (Claude valida):** DINOv2 vits14 sobre las mismas imágenes del
  manifest, mismo preprocesado (resize directo 224, norm ImageNet, L2-norm).
  `targets.npy` float32 (N,384) alineado por índice con `manifest.json`.
  Gate: N coincide, norma L2 ≈ 1, spot-check de 20 imágenes contra el harness.
- **F4 — Entrenamiento (usuario ejecuta Colab, Claude revisa):**
  Student = MobileNetV3-Large + `projection_head` 960→384 + BN + L2-norm. Capa de
  entrada que **hornea la normalización** (x en 0–255 → `(x-mean)/std`). DataLoader
  desde el manifest, `drop_last=True` (evita BN con batch 1). Augmentation **sólo
  geométrica** (flip H, crop leve) para no romper `align_loss`. Loss híbrido
  (cosine + relacional KL). Salida: `best_student_384.pth` + `training_log.json`
  (loss y métrica de validación por época). Gate: la validación mejora y estabiliza.
- **F5 — Export (Claude valida):** `litert-torch` (NO `ai_edge_torch`, que produce
  float32). FP16 vía `TFLiteConverter` con `optimizations=[Optimize.DEFAULT]` y
  `target_spec.supported_types=[tf.float16]`. Gate de paridad: mismo input →
  `cosine(PyTorch, TFLite) > 0.999`. Verificar: input float32 0–255, output 384, ~6 MB.
- **F6 — Gate de calidad (obligatorio):** registrar el modelo en `model_registry.py`
  y correr `extract_embeddings.py` + `evaluate.py` sobre el set 917. Criterio de
  aceptación: **mAP ≥ 0.79** (baseline) y nuevo umbral euclídeo calculado.
  Si no pasa → no se despliega.
- **F7 — Integración Flutter:** `HnswIndex(dimensions: 384)` + regenerar
  `objectbox.g.dart` + schema bump + re-escaneo total. Recalibrar `maxDistance`
  (hoy 0.85 en `vector_search_service.dart`) con el `euclidean_equiv` del harness.
  Actualizar localizaciones "960-dimensional" → 384. `min_build_number` forzado.
  Actualizar este `CLAUDE.md`.

### 17.3 Correcciones respecto a la propuesta original
- El modelo actual NO es Small/576: es **Large/960** (este documento estaba desactualizado).
- El destilado **no es drop-in** salvo que se hornee la normalización en el grafo.
- Faltaba criterio de aceptación medible → mAP ≥ baseline en el harness existente.
- Faltaba anti-fuga y manifest alineado → un desalineamiento de índice arruina todo.
- La conversión FP16 descrita era incorrecta (`ai_edge_torch` es float32; usar `litert-torch`).
- Augmentation vs. targets congelados: sólo geométrica.
- Reutilizar `tools/similarity_eval/`, no crear un pipeline nuevo.




