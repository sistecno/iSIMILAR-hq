# Instrucciones para la sesión de la app (`solopila/`) · próxima versión

Estado: listo para usar. Fuentes: `docs/definicion-tecnica.md` (Datos y privacidad),
`decisiones/2026-10-22-ficha-y-muro.md`, `borradores/2026-10-22-ficha-y-muro.md`.

## Cómo usarlo
1. Abre una terminal y entra en la carpeta de la app:
   `cd ~/Documents/Flutter/solopila && claude`
2. Pega este mensaje:
   > Lee `../iSIMILAR-hq/borradores/2026-10-22-instrucciones-app.md` y `../iSIMILAR-hq/docs/definicion-tecnica.md`.
   > Haz las tareas en el orden del archivo, una por una. Antes de cada una, explica qué
   > vas a cambiar, el riesgo y cómo deshacerlo, y espera mi autorización. Haz commit
   > después de cada tarea.
3. Revisa y autoriza cada tarea. Al final, prueba la app en un iPhone y en un Android.
4. Cuando termine, vuelve a la sesión de hq y di "app lista" para marcar las tareas como
   hechas en `borradores/pendientes.md`.

## Tareas (en este orden)

### Bloqueantes antes de publicar

**T1. Quitar Firebase Analytics**
- Quitar `firebase_analytics` de `pubspec.yaml` (línea 51).
- `lib/main.dart:22` llama a `AnalyticsService.init()`. Dejar `AnalyticsService` con los
  métodos de Firebase vacíos, sin importar `firebase_analytics`, como dice la definición
  técnica. Los atributos de RevenueCat (`paywall_trigger`, `batch_size`, `gallery_size`,
  `use_case`) **siguen funcionando**.
- Revisar `Podfile` (`$FirebaseAnalyticsWithoutAdIdSupport`) y `AndroidManifest.xml`
  (metadatos de Analytics y AD_ID) y quitar solo lo que sea de Analytics.
- Comprobar: `flutter pub deps | grep analytics` no devuelve nada, y la app compila en
  iOS y en Android.

**T2. Retrasar el token de notificaciones**
- iOS, `Info.plist`: `FirebaseMessagingAutoInitEnabled` = `NO`.
- Android, `AndroidManifest.xml`, dentro de `<application>`:
  `<meta-data android:name="firebase_messaging_auto_init_enabled" android:value="false" />`
- En `lib/services/notification_service.dart`, cuando el usuario active el recordatorio
  semanal y acepte el permiso: `FirebaseMessaging.instance.setAutoInitEnabled(true)` y
  pedir el token en ese momento. Si lo desactiva: `setAutoInitEnabled(false)` y
  `deleteToken()`.
- Revisar que `NotificationService.init()` (en `main.dart`) no pida el token al arrancar.
- **Importante:** hoy `lib/views/image_selection_view.dart:53` llama a
  `NotificationService.initFCM()` al abrir la pantalla principal, y `initFCM()`
  (`notification_service.dart:145`) pide el permiso de notificaciones en ese momento.
  Quitar esa llamada del `initState` y hacerla solo cuando el usuario active el
  recordatorio semanal. Al desactivarlo, llamar a `deleteToken()`.

**T3. Confirmar que no se usa Firebase Performance Monitoring**
- Buscar `firebase_performance` en `pubspec.yaml`, `Podfile.lock` y Gradle. Informar del
  resultado; no cambiar nada si no está.

**T4. Precio de respaldo $12.99**
- `lib/services/premium_service.dart:84-92` y `lib/views/widgets/premium_offer_sheet.dart:638, 665, 741`.
- El muro debe mostrar solo el precio que devuelve la tienda a través de RevenueCat.
  Si no llega, mostrar un estado de carga o error ("No se pudo cargar el precio") y no
  permitir comprar, nunca un precio escrito a mano.

**T4b. Interruptor para oponerse (decidido el 22-10)**
- En Ajustes: interruptor "Compartir datos técnicos para mejorar la app", activado por
  defecto y guardado en SharedPreferences. Texto debajo: "Informes de errores y datos de
  uso. Nunca tus fotos." Traducirlo a EN, ES e IT en los `.arb`.
- Al desactivarlo:
  - `FirebaseCrashlytics.instance.setCrashlyticsCollectionEnabled(false)`.
  - No enviar `paywall_trigger`, `batch_size`, `gallery_size` ni `use_case` a RevenueCat
    (en `AnalyticsService`), y no mostrar la pregunta tras la compra.
- Al arrancar la app, aplicar el valor guardado antes de enviar nada.
- Las compras y la restauración siguen funcionando: RevenueCat no se desactiva.

### Textos del muro de pago (`lib/l10n/intl_en.arb`, `intl_es.arb`, `intl_it.arb`)

**T5. `faq_a3` (precisión).** Probar las dos versiones en pantalla y quedarse con la que
quepa bien. Elegir la misma longitud en los 3 idiomas.

| | Larga | Corta |
|---|---|---|
| EN | Right about 8 times out of 10. It compares shape, texture, color and composition, so it finds photos that look alike, not one exact photo. Works best with photos taken in similar conditions: same angle, light and background. | Right about 8 times out of 10. Works best with photos taken in similar conditions: same angle, light and background. |
| ES | Acierta unas 8 de cada 10 veces. Compara forma, textura, color y composición: encuentra fotos que se parecen, no una foto exacta. Funciona mejor con fotos hechas en condiciones parecidas: mismo ángulo, misma luz y mismo fondo. | Acierta unas 8 de cada 10 veces. Funciona mejor con fotos hechas en condiciones parecidas: mismo ángulo, misma luz y mismo fondo. |
| IT | È precisa circa 8 volte su 10. Confronta forma, texture, colore e composizione: trova foto che si somigliano, non una foto esatta. Funziona meglio con foto scattate in condizioni simili: stessa angolazione, stessa luce e stesso sfondo. | È precisa circa 8 volte su 10. Funziona meglio con foto scattate in condizioni simili: stessa angolazione, stessa luce e stesso sfondo. |

**T6. `faq_a4` (sin conexión)**
- EN: "Yes. Searching for similar photos works without internet, even in airplane mode. Your photos never leave your device. You only need a connection to buy or restore PRO."
- ES: "Sí. La búsqueda de fotos parecidas funciona sin internet, incluso en modo avión. Tus fotos nunca salen del dispositivo. Solo necesitas conexión para comprar o restaurar PRO."
- IT: "Sì. La ricerca di foto simili funziona senza internet, anche in modalità aereo. Le tue foto non lasciano mai il dispositivo. Serve una connessione solo per acquistare o ripristinare PRO."

**T7. `faq_a5` (cancelación).** Usar el texto final en EN, ES e IT del apartado 5 de
`borradores/2026-10-22-legal-politicas-v3.md` (legal-tiendas), sin cambiarlo.

**T8. Limpieza (opcional).** Borrar las claves sin uso `all_trial_actions_used` y
`trial_footer_message` de los `.arb`, tras confirmar que no tienen referencias.

Después de T5–T8: regenerar `lib/generated/` (`flutter gen-l10n`) y comprobar que compila.

### Al publicar la versión (no es código)
- URLs de privacidad y términos: si ya existen `isimilar.app/privacy` y `/terms`, cambiar
  las URLs de Notion en `premium_offer_sheet.dart` y `settings_view.dart`. Si no, mantener
  Notion y dejarlo para la siguiente versión.
- Descripción de App Store: aplicar los cambios de `borradores/2026-10-22-ficha-y-muro.md`.
- `checklist-release` de hq antes de enviar a revisión.
