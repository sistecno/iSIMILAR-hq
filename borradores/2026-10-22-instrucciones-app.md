# Instrucciones para la sesión de la app (`solopila/`) · próxima versión

Estado: listo para usar (actualizado el 2026-10-23: T4c, T4d, T4e). Fuentes: `docs/definicion-tecnica.md` (Datos y privacidad),
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
  Si no llega, mostrar un estado de carga o error ("No se pudo cargar el precio"), nunca
  un precio escrito a mano.
- El botón de compra sigue siempre activo (decisión A del 2026-10-30,
  `decisiones/2026-10-30-boton-pago-sin-precio.md`). Al pulsarlo sin producto cargado:
  spinner y nueva petición a la tienda; si llega, el muro muestra el precio real y se abre
  la compra nativa; si no, mensaje "Sin conexión con la tienda, inténtalo de nuevo"
  (EN/ES/IT), nunca un fallo silencioso. Mientras no se sepa si hay prueba, el botón usa
  un texto neutro, no "Desbloquear todo".

**T4b. Interruptor para oponerse (decidido el 22-10)**
- En Ajustes: interruptor "Compartir datos técnicos para mejorar la app", activado por
  defecto y guardado en SharedPreferences. Texto debajo: "Informes de errores y datos de
  uso. Nunca tus fotos." Traducirlo a EN, ES e IT en los `.arb`.
- Al desactivarlo:
  - `FirebaseCrashlytics.instance.setCrashlyticsCollectionEnabled(false)`.
  - No enviar `paywall_trigger`, `batch_size`, `gallery_size` ni `use_case` a RevenueCat
    (en `AnalyticsService`), y no mostrar la pregunta tras la compra.
  - Borrar de RevenueCat los atributos ya enviados (`paywall_trigger`, `batch_size`,
    `gallery_size`, `use_case`) enviándolos vacíos (opción B, decidida por Anibal el
    2026-10-31). Comprobar que el borrado llega también si se desactiva sin red.
- Al arrancar la app, aplicar el valor guardado antes de enviar nada.
- Las compras y la restauración siguen funcionando: RevenueCat no se desactiva.

**T4c. Compartir en lote es PRO (añadido el 2026-10-23)**
- Hoy `lib/views/widgets/album_detail_sheet.dart:72-87` comparte varias fotos sin comprobar
  PRO ni abrir el muro (lo detectó legal-tiendas). Brief, definición técnica, web y términos
  ya dicen que todas las acciones en lote son PRO; compartir una sola foto sigue gratis.
- Aplicar la misma comprobación que borrar y mover en lote en todos los puntos desde los que
  se comparten varias fotos (resultados de búsqueda y visor de álbumes).
- Al abrir el muro desde ahí, enviar `paywall_trigger` = `batch_share` (definición técnica,
  Medición: valor pendiente).

**T4f. Compartir en lote desde los resultados de búsqueda (añadido el 2026-10-25)**
- Hoy la barra de selección de los resultados (`image_selection_view.dart`, `BottomNavigation`)
  solo tiene borrar y mover ("Save Image"). Compartir varias fotos solo existe en el visor de
  álbumes. Brief, definición técnica y web ya lo anuncian desde los resultados.
- Añadir "Compartir" a la selección de resultados con la misma comprobación PRO que borrar y
  mover (`canPerformBatchAction`) y `paywall_trigger` = `batch_share`. Una sola foto se sigue
  compartiendo gratis desde el detalle (`full_image_dialog.dart`).
- Hacerla junto con T4c (misma comprobación y mismo trigger) y traducir el texto del botón.

**T4g. Redes en Ajustes: TikTok → YouTube y Facebook (añadido el 2026-10-26)**
- Hoy la sección "Social" de `settings_view.dart` (líneas ~171-183 y `_showTikTok`, ~645)
  abre `https://www.tiktok.com/@lifesolutionsapp`. Quitar ese botón.
- Añadir dos botones con el mismo estilo (`_buildSocialButton`):
  - YouTube: `https://www.youtube.com/@iSIMILAR-APP` (icono genérico de vídeo, p. ej.
    `Icons.smart_display`; no añadir dependencias de iconos).
  - Facebook: `https://www.facebook.com/iSIMILAR/` (`Icons.facebook`).
- Textos en los `.arb` (sustituir `follow_tiktok*` por claves nuevas y borrar las viejas):

  | Clave | EN | ES | IT |
  |---|---|---|---|
  | `follow_youtube` | Watch us on YouTube | Síguenos en YouTube | Seguici su YouTube |
  | `follow_youtube_subtitle` | Tutorials and tips for using the app | Tutoriales y consejos para usar la app | Tutorial e consigli per usare l'app |
  | `follow_facebook` | Follow us on Facebook | Síguenos en Facebook | Seguici su Facebook |
  | `follow_facebook_subtitle` | News and updates | Novedades de la app | Novità dell'app |

- Abrir los enlaces fuera de la app, como hoy con TikTok. No envía datos.

**T4d. Enlaces legales a la web (añadido el 2026-10-23)**
- Las páginas ya están publicadas. Sustituir las URLs de Notion en `premium_offer_sheet.dart`
  y `settings_view.dart` por las de la web, en el idioma de la app:
  - EN: `https://isimilar.app/privacy/`, `/terms/`, `/delete-data/`
  - ES: `https://isimilar.app/es/privacy/`, `/es/terms/`, `/es/delete-data/`
  - IT: `https://isimilar.app/it/privacy/`, `/it/terms/`, `/it/delete-data/`
- Buscar cualquier otro enlace a Notion en `lib/` y en los `.arb`.

**T4e. Comprobar "Reset App" (añadido el 2026-10-23)**
- La página publicada de borrado de datos dice lo que hace "Reset App". Comprobar en el
  código que hace exactamente eso (índice, ajustes y álbumes creados desde la app) e
  informar. No cambiar nada sin autorización; si no coincide, se corrige la página.

**T4i. Restaurar compras sin compras que restaurar (aprobado el 2026-10-30)**
- Hoy, si "Restaurar compras" termina sin error pero no encuentra ninguna compra, el muro
  se cierra (`Navigator.pop` en `_purchase`) y el usuario no recibe ningún aviso. Parece
  un botón roto, y el revisor de Apple suele probarlo con una cuenta sin compras.
- Después de restaurar: si el usuario es PRO, se cierra el muro como hoy. Si sigue sin ser
  PRO, el muro queda abierto y se muestra este mensaje:

  | Clave | EN | ES | IT |
  |---|---|---|---|
  | `restore_nothing_found` | We couldn't find any purchases to restore. | No encontramos compras para restaurar. | Non abbiamo trovato acquisti da ripristinare. |

- Los errores de la restauración siguen el mismo criterio que T4 (error de red → mensaje
  traducido "Sin conexión con la tienda, inténtalo de nuevo").
- Commit propio, justo después del de T4. Probar en el iPhone con la cuenta sandbox
  caducada (sin compras activas).

**T4h. Entrar al muro desde la pantalla principal (aprobado el 2026-10-30)**
- Motivo: hoy el muro solo se abre al chocar con un límite (cámara, lote) o desde
  Ajustes. Quien no hace acciones y quiere comprar no encuentra cómo (caso real de un
  cliente). Hacer después de T4: el muro tiene que funcionar sin precio cargado.
- Solo para usuarios sin PRO. Los PRO no ven nada nuevo.
- **a) El contador se vuelve botón.** La pastilla naranja de
  `image_selection_view.dart:375-405` ("N búsquedas con cámara restantes") abre el muro
  al pulsarla, con `paywall_trigger` = `home_counter`. Que se vea pulsable: debajo del
  número, una segunda línea más pequeña con flecha:

  | Clave | EN | ES | IT |
  |---|---|---|---|
  | `home_counter_cta` | Unlimited with PRO › | Ilimitadas con PRO › | Illimitate con PRO › |

  Ojo: esta pastilla solo sale en la pantalla vacía (sin foto de referencia). Por eso
  hace falta también b).
- **b) Botón PRO fijo arriba.** En `custom_app_bar.dart`, a la derecha, una pastilla
  naranja (`0xFFFF6D00`) con `Icons.workspace_premium_rounded` y el texto "PRO", visible
  siempre que no se esté en modo selección. Abre el muro con `paywall_trigger` =
  `home_appbar`. Convive con el botón "Seleccionar". **Criterio de espacio (decidido por
  Anibal el 2026-10-31, tras las capturas):** el botón PRO conserva siempre su texto y, si
  no cabe todo, se reduce el título "iSIMILAR" (medido con resultados en español: 390 pt →
  30 pt, 375 pt → 26,9 pt, 360 pt → 23,7 pt). Solo por debajo de 360 pt (iPhone SE de
  1.ª generación) el botón PRO queda con el icono solo. Hecho en el commit 340dfdf.
- **Medición:** añadir `home_counter` y `home_appbar` al contrato de valores de
  `analytics_service.dart` (sección `paywall_trigger`). No renombrar los existentes.
- Nada de ventanas emergentes ni avisos automáticos: solo puntos de entrada visibles.

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
- En App Store Connect y Google Play Console: URL de privacidad `https://isimilar.app/privacy/`
  y, en Google Play, URL de borrado de datos `https://isimilar.app/delete-data/`.
- Descripción de App Store: aplicar los cambios de `borradores/2026-10-22-ficha-y-muro.md`.
- `checklist-release` de hq antes de enviar a revisión.
