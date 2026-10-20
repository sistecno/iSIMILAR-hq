# iSIMILAR (solopila) — App Flutter

> Índice para Claude. Mantener por debajo de 100 líneas: el detalle vive en `docs/`.
> Última reorganización: octubre 2026 (el CLAUDE.md anterior se dividió sin perder texto).

**Qué es:** buscador visual 100% en el dispositivo. El usuario elige UNA imagen base
(o usa la cámara) y la app encuentra las visualmente similares en su galería.
Regla de oro: siempre existe una imagen base. Detalle: `docs/arquitectura/concepto.md`.

## Stack real (las versiones mandan en `pubspec.yaml`)
Flutter · Provider (MVVM: `lib/views`, `lib/viewmodels`, `lib/services`) ·
TFLite MobileNetV3-Large 960 dims en Isolate · ObjectBox + HNSW · photo_manager ·
RevenueCat (`purchases_flutter`) · Firebase (Crashlytics, Messaging, Remote Config,
Analytics) · l10n EN/ES/IT en `lib/l10n/*.arb`.

## Comandos
- `flutter pub get` · `flutter run` · `flutter analyze` · `flutter test`
- Tras cambiar entidades ObjectBox: `dart run build_runner build --delete-conflicting-outputs`
- Tras cambiar `.arb`: `flutter gen-l10n` (salida en `lib/generated/`)
- Evaluación del modelo: `tools/similarity_eval/` (ver su README)

## Dónde está cada cosa (leer solo cuando haga falta)
| Tema | Archivo |
|---|---|
| Modelo IA, aceleración GPU/CoreML | `docs/arquitectura/stack-y-modelo-ia.md` |
| ObjectBox, entidades, datos locales | `docs/arquitectura/objectbox-y-datos.md` |
| Escaneo, búsqueda, memes, acciones | `docs/arquitectura/escaneo-busqueda-acciones.md` |
| Monetización y verificación de trials | `docs/arquitectura/monetizacion.md` |
| Notificaciones y actualizaciones forzadas | `docs/arquitectura/notificaciones-y-actualizaciones.md` |
| Notas de UX aprobadas | `docs/arquitectura/ux-aprobada.md` |
| Decisiones registradas | `docs/decisiones/` |
| Pendientes técnicos | `docs/BACKLOG.md` |
| Bitácora | `HISTORY.md` |
| Plan original ya completado | `docs/archivo/` (no usar como fuente) |

Varios docs de arquitectura tienen partes antiguas (créditos, versiones, tiempos).
Si un doc contradice al código, manda el código; avisar y proponer corregir el doc.
Negocio, marketing y legal viven en `../iSIMILAR-hq/` (no aquí).

## ⭐ Proyecto activo: destilación DINOv2 → MobileNetV3
Plan completo, decisiones cerradas y puntos de control F0.5–F7 en
`tools/distill/ROADMAP.md`. **Leerlo antes de tocar `tools/`, el modelo `.tflite`,
`embedding_service.dart`, `vector_search_service.dart` o el schema de ObjectBox.**
Gate obligatorio: mAP ≥ 0.79 sobre el set de 917 antes de desplegar.

## Reglas de Colaboración con Claude

### Ante ideas nuevas
Cuando el usuario presente una idea nueva, Claude DEBE:
1. Registrarla en `docs/decisiones/AAAA-MM-DD-tema.md` (NO en este archivo).
2. Cuestionar la idea con lógica — pros, contras, riesgos reales.
3. Destruir los argumentos débiles con evidencia o razonamiento, sin importar quién los proponga.
4. Hacer preguntas serias y verificables con el objetivo de encontrar el plan óptimo, no de validar la idea original.

### Modo de respuesta
- **No seguir la corriente.** Si una idea tiene un fallo, decirlo directamente.
- **Decir lo que se necesita escuchar, no lo que se quiere escuchar.**
- **Contradecir y criticar cuando corresponda** — sin miedo, sin suavizar.
- **Cero sesgo de complacencia** hacia el usuario.
- El objetivo es el mejor resultado posible para el producto, no la aprobación del usuario.

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

## Reglas de trabajo
- No tocar código ni el repo sin una orden clara (ver directriz en `HISTORY.md`).
- Cambios de schema ObjectBox o de modelo → versión propia + `min_build_number`.
- Textos visibles siempre en EN, ES e IT a la vez.
- Al terminar algo relevante: entrada en `HISTORY.md`; nunca crecer este archivo.
