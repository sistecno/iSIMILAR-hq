> ⚠️ Texto copiado íntegro del antiguo CLAUDE.md (oct 2026). Algunas partes están desactualizadas (créditos, versiones, dimensiones, tiempos). Ante cualquier duda manda el código; resumen vigente en `../iSIMILAR-hq/docs/definicion-tecnica.md`.


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
