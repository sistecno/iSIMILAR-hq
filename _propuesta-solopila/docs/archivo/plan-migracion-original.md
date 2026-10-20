# Archivo: plan original de migración (completado)


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

## Pre-lanzamiento — Checklist
[x] Botón "Restaurar Compras" — implementado en PremiumOfferSheet footer.
[x] Privacy Policy URL en la ficha de la tienda — configurado.
[x] Permiso NSPhotoLibraryUsageDescription en Info.plist — configurado.
[x] Manejo de permisos Android 13 (READ_MEDIA_IMAGES) vs Android <13 — resuelto.
[x] Crashlytics configurado para capturar errores dentro del Isolate — resuelto.
[x] Actualizaciones forzadas configuradas (Firebase Remote Config min_build_number) — activo.
[x] App Store ID obtenido y URLs de tienda definidas — app publicada en ambas tiendas.
