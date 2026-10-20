# Backlog técnico


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
