> ⚠️ Texto copiado íntegro del antiguo CLAUDE.md (oct 2026). Algunas partes están desactualizadas (créditos, versiones, dimensiones, tiempos). Ante cualquier duda manda el código; resumen vigente en `../iSIMILAR-hq/docs/definicion-tecnica.md`.


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
