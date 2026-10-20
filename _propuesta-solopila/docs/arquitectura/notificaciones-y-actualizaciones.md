> ⚠️ Texto copiado íntegro del antiguo CLAUDE.md (oct 2026). Algunas partes están desactualizadas (créditos, versiones, dimensiones, tiempos). Ante cualquier duda manda el código; resumen vigente en `../iSIMILAR-hq/docs/definicion-tecnica.md`.


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
