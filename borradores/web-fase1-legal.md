# Web Fase 1 · Privacidad y términos (borrador de legal-tiendas)

Fecha: 2026-10-21 · Estado: BORRADOR, pendiente de revisión de Anibal y de `tono-de-marca`.
Origen: `decisiones/2026-10-21-web-astro-seo.md` (Fase 1).

> **Aviso:** esto no es asesoramiento legal definitivo. Los puntos marcados **[ABOGADO]**
> necesitan revisión de un abogado de protección de datos / consumo en Italia antes de publicar.
> Los marcados **[COMPLETAR]** necesitan un dato que no tengo.

---

## 0. Qué he podido leer y qué no

| Fuente | Resultado |
|---|---|
| Notion · Privacidad (`.../Privacy-Policy-for-iSIMILAR-13d88278a02e804aa1a0cbf3b661a05d`) | **No he podido leer el texto.** WebFetch solo recibe el armazón JavaScript de Notion ("Notion"). |
| Notion · Términos (`.../Terms-and-Conditions-for-iSIMILAR-13d88278a02e80e4b5f8d790f9d388f1`) | **No he podido leer el texto.** Mismo motivo. Tampoco hay copia indexada en buscadores. |
| Buscador (solo fragmentos indexados de la página de privacidad) | Aparecen **dos versiones**: una "Last updated: March 2026" (procesamiento en el dispositivo; embeddings guardados localmente; desarrollador citado como "Creadores de Ventas") y otra fechada 2024-12-01 que dice que la app "no recoge ningún dato personal" y que usa Google ML Kit Image Labeling. **No puedo confirmar cuál es la vigente ni su texto completo.** |
| Código de `../solopila/` | Leído: `analytics_service.dart`, `premium_service.dart`, `premium_offer_sheet.dart`, `settings_view.dart`, `notification_service.dart`, `main.dart`, `pubspec.yaml`, `ios/Podfile`, `ios/Runner/Info.plist`, `AndroidManifest.xml`. |
| Web publicada `../solopila_landingPAGE/web/` | Leído el pie de página e `i18n.js`. |

**Consecuencia:** la auditoría de los textos de Notion (apartado 1.B) es **condicional**: lista lo que
deben decir y lo que no pueden decir según los documentos de `docs/`, y qué hay que comprobar a mano.
Para cerrarla, Anibal tiene que pegar aquí el texto de ambas páginas (o exportarlas a Markdown desde Notion).

---

## 1. Auditoría

### 1.A Riesgos ordenados (rechazo o sanción primero)

| # | Requisito | Estado | Evidencia | Acción |
|---|---|---|---|---|
| 1 | La política describe con exactitud todos los datos que salen del dispositivo y todos los terceros (Apple 5.1.1(i); Google Play "User Data › Privacy Policy"; RGPD arts. 13-14) | **No cumple** (probable) | El código usa 5 SDK que envían datos: RevenueCat, Crashlytics, Remote Config, Cloud Messaging (FCM) y Analytics (`pubspec.yaml:45-51`). `docs/definicion-tecnica.md` solo lista 3. Los fragmentos indexados de Notion (marzo 2026) son anteriores a los atributos de RevenueCat y a Analytics. | Publicar el texto del apartado 2. Ver Contradicción C2. |
| 2 | Etiqueta App Store "datos no vinculados" coherente con la definición de Apple | **Riesgo / sin verificar** | Apple (App Privacy Details): "'Personal Information' and 'Personal Data', as defined under relevant privacy laws, are considered linked to the user." El documento dice a la vez que son datos seudónimos (personales para el RGPD) y que la etiqueta los declara "no vinculados". | Ver Contradicción C4. **[ABOGADO]** |
| 3 | Base jurídica de Firebase Analytics en la UE sin pedir consentimiento | **Riesgo / sin verificar** | `analytics_service.dart:60-67`: `analyticsStorageConsentGranted: true` sin pregunta al usuario. El art. 5(3) de la Directiva ePrivacy (en Italia, art. 122 del Codice privacy) exige consentimiento para leer/guardar información en el terminal salvo que sea estrictamente necesario. EDPB Guidelines 2/2023 (versión 2.0, 16-10-2024) tratan el alcance técnico; **no he podido leer el texto final sobre SDK de apps**. | **[ABOGADO]** antes de publicar la versión con Analytics: ¿interés legítimo o consentimiento (pantalla de opt-in)? |
| 4 | Política en URL pública, activa, no geobloqueada, no PDF (Google Play "User Data › Privacy Policy") | **Sin verificar** | Notion responde, pero su contenido solo se ve con JavaScript: buscadores y asistentes de IA no lo leen bien. Funciona para el revisor humano. | Migrar a `/privacy` (apartado 3). |
| 5 | Enlaces a privacidad y términos en la app y en los metadatos de la tienda (Apple 5.1.1(i); developer.apple.com/app-store/subscriptions: "your app and App Store metadata must include links to your Terms of Use and Privacy Policy") | **Cumple en la app / sin verificar en la tienda** | Muro de pago: `premium_offer_sheet.dart:894-927` enlaza privacidad y términos (Notion). Ajustes: `settings_view.dart:652-664`. No puedo ver App Store Connect ni Play Console. | Comprobar a mano el campo de URL de privacidad y el enlace a Terms of Use (descripción o campo EULA) en App Store Connect. |
| 6 | Muro de pago: nombre, duración, precio de renovación visible y localizado; prueba con duración y precio tras la prueba; restaurar compras (developer.apple.com/app-store/subscriptions; App Review 3.1.1 y 3.1.2(c); Google Play, política de suscripciones answer/9900533) | **Cumple en lo esencial, con 2 defectos** | Precio de la tienda como elemento mayor (`premium_offer_sheet.dart:638`, 32 pt) y desglose mensual subordinado (14 pt). Pie de prueba EN: "Today: $0.00. Then {fullPrice}/year after 7 days. Cancel anytime before your trial ends…". "Subscriptions renew automatically" (`intl_en.arb:409`). Botón "Restore Purchases" (`:860-881`). **Defecto a:** si la tienda no responde se muestra `$12.99` fijo (C3). **Defecto b:** ES dice "Hoy: $0.00" a usuarios que pagan en euros (`intl_es.arb:548`). | Corregir el precio de respaldo y la moneda fija (sesión en `solopila/`). |
| 7 | Gestión/cancelación de la suscripción accesible (Google Play answer/9900533: "link to manage and cancel subscriptions in the account setting or equivalent page") | **Cumple** | `credits_hero.dart:127-129` enlaza a las suscripciones de App Store y Google Play. | Ninguna. |
| 8 | Sin rastreo, sin IDFA/AD_ID (Apple 5.1.2(i)) | **Cumple** | `Podfile:9` `$FirebaseAnalyticsWithoutAdIdSupport = true`; `AndroidManifest.xml:21` elimina `AD_ID`; `:51-53` `google_analytics_adid_collection_enabled=false`; consentimiento de señales publicitarias denegado (`analytics_service.dart:64-66`); `Info.plist` no tiene `NSUserTrackingUsageDescription`. | Mantener. |
| 9 | Terminología: "seudónimos", nunca "anónimos" ni "cero datos" | **No cumple en la web** | Pie de la web: "Privacy Policy (100% local processing)" (`i18n.js:96`, `:192`, `:288`) y enlaces a `#` (`index.html:191`). | Ver Contradicción C1. |
| 10 | Forma de pedir el borrado y de retirar el consentimiento (Apple 5.1.1(i); RGPD art. 17) | **Sin verificar** | Existe una tercera página en Notion: `Data-Deletion-iSimilar-32388278a02e80f3a0f6c6cf12028e33` (`settings_view.dart:664`). No he podido leerla. El ID de RevenueCat se copia con pulsación larga en la versión (`settings_view.dart:273-275`), útil para localizar los datos. | Incluir el procedimiento en `/privacy` (apartado 2) y migrar también esa página. |
| 11 | Identificación del responsable del tratamiento (RGPD art. 13.1.a; Google Play: "Developer information and a privacy point of contact") | **Sin verificar** | El fragmento indexado de Notion cita "Creadores de Ventas". **No puedo confirmar** si es el titular correcto, ni su forma jurídica, dirección o P. IVA. | **[COMPLETAR] [ABOGADO]** |
| 12 | Transferencias a EE. UU. (Google/Firebase, RevenueCat) | **Sin verificar** | No he encontrado la certificación de RevenueCat en el EU-US Data Privacy Framework; su DPA existe (revenuecat.com/dpa). | **[COMPLETAR] [ABOGADO]**: mecanismo de transferencia de cada proveedor. |
| 13 | Plazos de conservación (RGPD art. 13.2.a; Google Play; Apple 5.1.1(i)) | **Sin verificar** | Dependen de la configuración de cada consola (Firebase, RevenueCat). No puedo verlas. | **[COMPLETAR]** desde las consolas. |
| 14 | Derecho de desistimiento de 14 días (Directiva 2011/83/UE) y reembolsos | **Sin verificar** | Las compras las procesan Apple y Google. | **[ABOGADO]** redacción de la cláusula. |
| 15 | Manifiesto de privacidad iOS (`PrivacyInfo.xcprivacy`) a nivel de app | **Sin verificar** | No existe en `ios/Runner/`. Los SDK suelen traer el suyo. | Revisar en la sesión de `solopila/` con `checklist-release`. Fuera del alcance de la web. |

### 1.B Auditoría condicional de los textos de Notion (no he podido leerlos)

Cuando Anibal pegue los textos, comprobar punto por punto:

**Política de privacidad: debe decir**
- Las fotos, miniaturas y vectores nunca salen del teléfono.
- Los 5 servicios y lo que recibe cada uno (tabla del apartado 2). Si solo nombra RevenueCat y Crashlytics, está incompleta (faltan Remote Config y Cloud Messaging, que están en el código desde marzo de 2026 según el historial de git; y Analytics en cuanto se publique).
- Los atributos de RevenueCat (`paywall_trigger`, `batch_size`, `gallery_size`, `use_case`), añadidos en octubre de 2026: casi seguro **ausentes** si la última versión es de marzo de 2026.
- Que los datos son **seudónimos** (asociados a un identificador), no anónimos.
- Responsable, contacto, bases jurídicas, transferencias, conservación, derechos, autoridad de control (Garante per la protezione dei dati personali), cómo pedir el borrado.
- Que los terceros ofrecen una protección equivalente (Apple 5.1.1(i), segundo punto).

**Política de privacidad: no puede decir** (si aparece, es contradicción con `definicion-tecnica.md` · "Datos y privacidad" y `brief-marketing.md` · "Lo que se puede y no se puede decir")
- "No recogemos ningún dato personal", "zero data", "datos anónimos", "100% local processing", "nada sale de tu teléfono".
- "Google ML Kit Image Labeling" o que la app etiqueta objetos (el fragmento de 2024 lo dice; el modelo real es MobileNetV3-Large en TFLite).
- Cualquier mención a publicidad, IDFA o rastreo.

**Términos: deben decir**
- Plan gratuito y PRO exactamente como en `definicion-tecnica.md` · "Modelo comercial".
- Suscripción **anual**, prueba de **7 días**, renovación automática, cómo cancelar, que el cobro lo hace la tienda.
- Ninguna mención a créditos, paquetes de créditos, "5 free actions" ni precio 12,99 USD.
- Que la búsqueda es por parecido visual, con precisión limitada (no "foto exacta", no "alta precisión"), y que el usuario confirma cada borrado.

### 1.C Contradicciones detectadas

⚠️ Contradicción detectada (C1)
- Documento: `docs/definicion-tecnica.md` · "Datos y privacidad" dice: RevenueCat recibe compras, un identificador seudónimo y atributos; Crashlytics recibe errores y rendimiento. `docs/brief-marketing.md` · "Lo que se puede y no se puede decir" prohíbe "Cero recopilación de datos".
- Fuente: web publicada `solopila_landingPAGE/web/i18n.js · líneas 96, 192, 288` dice: "Privacy Policy (100% local processing)" / "Política de Privacidad (procesamiento 100% local)" / "Informativa sulla Privacy (elaborazione 100% locale)"; `index.html · línea 191` enlaza a `#`.
- Impacto: afirmación falsa sobre el tratamiento de datos en el propio enlace a la política; enlace roto a privacidad y términos.
- Opciones: A) ajustar la fuente al documento (en la web nueva el pie dirá solo "Privacy Policy" / "Terms" y enlazará a `/privacy` y `/terms`) · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada (C2)
- Documento: `docs/definicion-tecnica.md` · "Arquitectura" y "Datos y privacidad" dice: los servicios que reciben datos son RevenueCat, Firebase Crashlytics y (próxima versión) Firebase Analytics.
- Fuente: `solopila/pubspec.yaml · líneas 47-48` incluye `firebase_messaging` y `firebase_remote_config`; `lib/services/notification_service.dart · línea 144` inicializa Firebase Cloud Messaging y pide permiso (llamado en `image_selection_view.dart · línea 53`); `lib/services/force_update_service.dart · línea 8` usa Remote Config. Según la documentación de Firebase (firebase.google.com/docs/ios/app-store-data-collection), Cloud Messaging recoge el token APNs asociado a un ID de instalación, modelo, idioma, zona horaria y versión del SO; Remote Config recoge código de país, idioma, zona horaria y versión del SO.
- Impacto: la política, la etiqueta de la App Store y el formulario de Google Play pueden estar incompletos (Device ID / identificadores). Es un riesgo de rechazo y de incumplimiento del art. 13 RGPD.
- Opciones: A) ajustar la fuente al documento (quitar FCM y/o Remote Config del código) · B) Anibal revisa el documento para añadir ambos servicios a la tabla de "Datos y privacidad". El texto propuesto en el apartado 2 ya los incluye, a la espera de esta decisión.
- Esperando decisión.

⚠️ Contradicción detectada (C3)
- Documento: `docs/definicion-tecnica.md` · "Modelo comercial en el código" dice: PRO cuesta 11,99 USD en EE. UU. `docs/brief-marketing.md` · "Precio" dice: el precio debe ser el mismo en la app, la tienda y la web.
- Fuente: `solopila/lib/services/premium_service.dart · líneas 84-85 y 90-91` y `lib/views/widgets/premium_offer_sheet.dart · líneas 638, 665 y 741` usan `$12.99` / `12.99` como valor de respaldo cuando la tienda no devuelve el precio.
- Impacto: si falla la consulta a la tienda, el muro de pago muestra un precio que no es el que se cobra. Apple exige que el precio de renovación sea claro y correcto; mostrar un importe falso es riesgo de rechazo (3.1.2) y de práctica engañosa.
- Opciones: A) ajustar la fuente al documento (no mostrar precio fijo; si no hay precio de la tienda, desactivar el botón de compra) · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada (C4)
- Documento: `docs/definicion-tecnica.md` · "Datos y privacidad" dice: "Etiqueta de privacidad actual en la App Store: datos no vinculados a la persona" y, en "Terminología", que esos datos "para el RGPD son datos seudónimos, no anónimos".
- Fuente: Apple, developer.apple.com/app-store/app-privacy-details, sección "Data linked to the user", dice: "'Personal Information' and 'Personal Data', as defined under relevant privacy laws, are considered linked to the user." Los datos seudónimos son datos personales según el RGPD (considerando 26).
- Impacto: la etiqueta "no vinculados" podría no ser exacta según la propia definición de Apple. Apple puede pedir corrección; y la etiqueta es lo que ChatGPT y los usuarios leen. Cambiar a "vinculados" no implica rastreo ni publicidad.
- Opciones: A) ajustar la fuente al documento (mantener "no vinculados" y documentar por qué: sin cuenta, sin nombre ni correo, ID aleatorio de RevenueCat) · B) Anibal revisa el documento para declarar "vinculados a la persona, sin rastreo" en la etiqueta. **[ABOGADO]** recomendado.
- Esperando decisión.

⚠️ Contradicción detectada (C5)
- Documento: `docs/definicion-tecnica.md` · "Límites conocidos" dice: precisión en torno al 80%; funciona mejor con la misma luz, fondo y ángulo. `docs/brief-marketing.md` prohíbe "Búsqueda de alta precisión" (vía guía) y promesas sin respaldo.
- Fuente: `solopila/lib/l10n/intl_en.arb · línea 462` (FAQ del muro de pago) dice: "How accurate is the search? Very. … A circuit board is a circuit board from any angle."
- Impacto: promesa en el propio muro de pago, justo antes de cobrar. Riesgo de reseñas negativas y de queja por publicidad engañosa.
- Opciones: A) ajustar la fuente al documento · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada (C6, condicional: no puedo confirmar que siga publicada)
- Documento: `docs/definicion-tecnica.md` · "Arquitectura" y "Datos y privacidad" dice: modelo MobileNetV3-Large en TFLite; RevenueCat y Crashlytics reciben datos.
- Fuente: versión de la política de Notion indexada en buscadores, fechada 2024-12-01, dice (según el fragmento): la app "no recoge ningún dato personal" y usa "Google ML Kit Image Labeling API".
- Impacto: si esa versión sigue visible en Notion o en el historial, la política es falsa en lo esencial.
- Opciones: A) ajustar la fuente al documento (se sustituye por el texto del apartado 2) · B) Anibal revisa el documento
- Esperando decisión (y que Anibal confirme qué versión está publicada).

**Nota, no contradicción:** `definicion-tecnica.md` · "Pendiente de confirmar" pregunta si "quitar de un álbum" se registra como `remove_album`. El código lo resuelve: existe `actionRemoveAlbum = 'remove_album'` (`analytics_service.dart:39`). La tabla de eventos del documento solo lista `delete`, `move_album`, `share`. Lo decide Anibal.

**Nota, no puedo confirmar:** el código del repositorio ya integra Firebase Analytics (`main.dart:22`, `analytics_service.dart`). El historial de git no muestra ese cambio confirmado, así que probablemente no está publicado (la última versión registrada es 1.1.6+28). Si estuviera publicado, la política y las etiquetas ya irían tarde.

---

## 2. Propuesta de texto: `/privacy` y `/terms`

Notas de montaje (para la sesión de Astro):
- HTML estático, texto en la página (sin cargar idiomas por JavaScript). `<html lang="en|es|it">`, `hreflang` entre las tres versiones, `<link rel="canonical">`.
- Rutas: `/privacy`, `/terms` (EN); `/es/privacy`, `/es/terms`; `/it/privacy`, `/it/terms`. Las rutas en inglés también en ES/IT para que los enlaces sean predecibles (alternativa: `/es/privacidad`; decide `growth`).
- La sección "Delete your data" lleva un ancla (`/privacy#delete`) para sustituir la página de Notion de borrado.
- Los bloques marcados **[NEXT VERSION · Firebase Analytics]** solo se publican el mismo día que la versión de la app con Analytics (ver 2.7).
- Sustituir todos los **[COMPLETAR]** antes de publicar. No publicar con corchetes.

### 2.1 Privacy Policy (EN, versión principal)

```
# iSIMILAR Privacy Policy

Last updated: [COMPLETAR: fecha de publicación]

iSIMILAR is a visual search app for the photos on your phone. This policy explains what
data the app uses, what leaves your device, and your rights.

## The short version

- Your photos never leave your phone. Photos, thumbnails and the visual "fingerprints"
  (vectors) the app calculates are created and stored only on your device.
- We do not have an account system. We never ask for your name, email or phone number.
- The app sends a limited set of technical data about purchases, usage and errors to the
  service providers listed below. This data is linked to a random identifier, not to your
  name. Under the EU General Data Protection Regulation (GDPR) it is pseudonymous data,
  not anonymous data.
- We do not use your data for advertising, we do not track you across other apps or
  websites, we do not collect the advertising identifier (IDFA on iOS, Advertising ID on
  Android), and we do not sell your data.

## Who is responsible

Data controller: [COMPLETAR: nombre o razón social, forma jurídica]
Address: [COMPLETAR: dirección postal en Italia]
VAT number: [COMPLETAR: P. IVA, si aplica]
Contact for privacy questions: info@isimilar.app

## What stays on your device

- Your photos and any album you create or change.
- Thumbnails (224 px) used to analyse your photos.
- The vectors (lists of numbers that describe what a photo looks like) and the search
  index. They are stored in a local database on your phone and are deleted when you
  uninstall the app.
- Photos you take with the camera to search.

The visual analysis runs entirely on your phone, with or without an internet connection.
None of this is sent to us or to any third party.

## What leaves your device, and why

| Service (provider) | What it receives | Why |
|---|---|---|
| RevenueCat (RevenueCat, Inc., USA) | Your purchase and subscription status, a random user ID created by RevenueCat, and these measurement fields: what opened the upgrade screen (camera, batch delete, batch move to album, settings), how many photos were selected, the size of your gallery as a range (under 3,000, 3,000-10,000, over 10,000) and, if you choose to answer, what you use the app for. | To process and restore your subscription, and to understand which features lead people to upgrade. |
| Firebase Crashlytics (Google) | Crash reports and performance data: technical details of the error, app version, device model and operating system version, linked to an installation identifier. | To find and fix errors. |
| Firebase Remote Config (Google) | App version, operating system version, country and language settings, linked to an installation identifier. | To tell you when an update is required. |
| Firebase Cloud Messaging (Google) | A notification token for your device, device model, language, time zone and operating system version. Only if you allow notifications. | To deliver notifications. |
| [NEXT VERSION · Firebase Analytics] Google Analytics for Firebase (Google) | Usage events: scan started or completed (number of photos and duration), search from gallery or camera, actions on photos (delete, move to album, remove from album, share; number of photos; whether it was a batch action), upgrade screen shown and the answer about how you use the app, linked to an app-instance identifier. No photos, thumbnails, vectors or image content. Collection of the advertising identifier is disabled and advertising signals are set to "denied". | To understand how the app is used and improve it. |

None of these services receives your photos, thumbnails, vectors, file names, locations
stored in your photos, or any other content of your gallery.

Payments are processed by Apple (App Store) or Google (Google Play). We never see your
card or bank details; we only receive the status of your purchase through RevenueCat.

Each of these providers processes data on our behalf under a data processing agreement
and is required to protect it at least to the level described in this policy.

## Permissions the app asks for

- Photos: to scan and search your gallery on your device, and to delete, move or share
  photos when you confirm it. Required for the app to work.
- Camera: to take a photo and use it as a search. Optional; the photo stays on your phone.
- Notifications: for the optional weekly reminder and notices about the app. Optional.

## Legal basis (GDPR)

- Processing your subscription: performance of a contract (Art. 6(1)(b) GDPR).
- Crash reports, required-update checks and measurement of what leads to an upgrade:
  our legitimate interest in keeping the app working and improving it (Art. 6(1)(f)).
- Notifications: your consent, given through your phone's permission prompt
  (Art. 6(1)(a)). You can withdraw it at any time in your phone's settings.
- [NEXT VERSION · Firebase Analytics] Usage analytics: [ABOGADO: interés legítimo
  (Art. 6(1)(f)) o consentimiento (Art. 6(1)(a)) — decidir antes de publicar].

## International transfers

RevenueCat and Google may process data in the United States. These transfers rely on
[COMPLETAR/ABOGADO: EU-US Data Privacy Framework y/o cláusulas contractuales tipo
de la Comisión Europea, por proveedor].

## How long we keep data

- RevenueCat: [COMPLETAR] (purchase records may need to be kept as long as required by
  tax and accounting law).
- Firebase Crashlytics: [COMPLETAR, según consola].
- [NEXT VERSION · Firebase Analytics] Firebase Analytics: [COMPLETAR, según la
  configuración de retención en la consola].
- Data on your device: until you delete it or uninstall the app.

## Your rights

You can ask us to access, correct or delete your data, to restrict or object to its
processing, and to receive a copy of it (Arts. 15-21 GDPR). Where processing is based on
consent, you can withdraw it at any time. You can also complain to the Italian data
protection authority (Garante per la protezione dei dati personali, garanteprivacy.it) or
to the authority in the EU country where you live.

## Delete your data {#delete}

- On your phone: uninstall iSIMILAR. This deletes the index, vectors and settings stored
  by the app. Your photos are not affected.
- On our providers: email info@isimilar.app with the subject "Delete my data" and your
  iSIMILAR user ID. To copy it, open Settings in the app and press and hold the version
  number at the bottom. We will delete the data linked to that ID from RevenueCat and
  Firebase within [COMPLETAR: plazo, máximo 1 mes según art. 12.3 RGPD], except purchase
  records we must keep by law.
- Deleting your data does not cancel your subscription. To cancel, use your App Store or
  Google Play subscription settings.

## Children

iSIMILAR is not directed at children under [COMPLETAR/ABOGADO: 14, edad de
consentimiento digital en Italia] and we do not knowingly collect data from them.

## Changes

If we change how the app uses data, we will update this page and the date above before
the change reaches the app.

## Contact

info@isimilar.app
```

### 2.2 Política de privacidad (ES)

```
# Política de privacidad de iSIMILAR

Última actualización: [COMPLETAR]

iSIMILAR es una app de búsqueda visual para las fotos de tu teléfono. Esta política
explica qué datos usa la app, qué sale del dispositivo y cuáles son tus derechos.

## En resumen

- Tus fotos nunca salen del teléfono. Las fotos, las miniaturas y las "huellas" visuales
  (vectores) que calcula la app se crean y se guardan solo en tu dispositivo.
- No hay cuentas de usuario. Nunca te pedimos nombre, correo ni teléfono.
- La app envía un conjunto limitado de datos técnicos de compras, uso y errores a los
  proveedores que se indican abajo. Esos datos van asociados a un identificador aleatorio,
  no a tu nombre. Según el Reglamento General de Protección de Datos (RGPD) son datos
  seudónimos, no anónimos.
- No usamos tus datos para publicidad, no te rastreamos en otras apps ni webs, no
  recogemos el identificador publicitario (IDFA en iOS, ID de publicidad en Android) y no
  vendemos tus datos.

## Responsable

Responsable del tratamiento: [COMPLETAR]
Dirección: [COMPLETAR]
P. IVA: [COMPLETAR]
Contacto de privacidad: info@isimilar.app

## Qué se queda en tu dispositivo

- Tus fotos y los álbumes que crees o modifiques.
- Las miniaturas (224 px) que se usan para analizar las fotos.
- Los vectores (listas de números que describen cómo es una foto) y el índice de
  búsqueda. Se guardan en una base de datos local y se borran al desinstalar la app.
- Las fotos que haces con la cámara para buscar.

El análisis visual se hace por completo en el teléfono, con o sin conexión. Nada de esto
se envía a nosotros ni a terceros.

## Qué sale del dispositivo y para qué

| Servicio (proveedor) | Qué recibe | Para qué |
|---|---|---|
| RevenueCat (RevenueCat, Inc., EE. UU.) | El estado de tu compra y suscripción, un identificador aleatorio creado por RevenueCat y estos campos de medición: qué abrió la pantalla de mejora (cámara, borrado en lote, mover en lote a un álbum, ajustes), cuántas fotos había seleccionadas, el tamaño de la galería por tramos (menos de 3.000, de 3.000 a 10.000, más de 10.000) y, si decides responder, para qué usas la app. | Gestionar y restaurar tu suscripción y entender qué funciones llevan a mejorar a PRO. |
| Firebase Crashlytics (Google) | Informes de errores y datos de rendimiento: detalles técnicos del error, versión de la app, modelo del dispositivo y versión del sistema, asociados a un identificador de instalación. | Encontrar y corregir errores. |
| Firebase Remote Config (Google) | Versión de la app y del sistema, país e idioma configurados, asociados a un identificador de instalación. | Avisarte cuando una actualización es obligatoria. |
| Firebase Cloud Messaging (Google) | Un token de notificaciones de tu dispositivo, modelo, idioma, zona horaria y versión del sistema. Solo si permites las notificaciones. | Enviar notificaciones. |
| [PRÓXIMA VERSIÓN · Firebase Analytics] Google Analytics para Firebase (Google) | Eventos de uso: escaneo iniciado o completado (número de fotos y duración), búsqueda desde la galería o la cámara, acciones sobre fotos (borrar, mover a un álbum, quitar de un álbum, compartir; número de fotos; si fue en lote), pantalla de mejora mostrada y la respuesta sobre el uso, asociados a un identificador de instancia de la app. Sin fotos, miniaturas, vectores ni contenido de las imágenes. La recogida del identificador publicitario está desactivada y las señales de publicidad, denegadas. | Entender cómo se usa la app y mejorarla. |

Ninguno de estos servicios recibe tus fotos, miniaturas, vectores, nombres de archivo,
ubicaciones guardadas en las fotos ni ningún otro contenido de tu galería.

Los pagos los procesa Apple (App Store) o Google (Google Play). Nunca vemos los datos de
tu tarjeta ni de tu banco; solo recibimos el estado de la compra a través de RevenueCat.

Cada proveedor trata los datos por cuenta nuestra con un contrato de encargo del
tratamiento y debe protegerlos al menos con el nivel que describe esta política.

## Permisos que pide la app

- Fotos: para escanear y buscar en tu galería dentro del teléfono, y para borrar, mover o
  compartir fotos cuando lo confirmas. Necesario para que la app funcione.
- Cámara: para hacer una foto y usarla como búsqueda. Opcional; la foto se queda en el
  teléfono.
- Notificaciones: para el recordatorio semanal opcional y avisos sobre la app. Opcional.

## Base jurídica (RGPD)

- Gestión de la suscripción: ejecución de un contrato (art. 6.1.b RGPD).
- Informes de errores, comprobación de actualizaciones obligatorias y medición de qué
  lleva a mejorar a PRO: nuestro interés legítimo en que la app funcione y mejore
  (art. 6.1.f).
- Notificaciones: tu consentimiento, dado en el aviso de permisos del teléfono
  (art. 6.1.a). Puedes retirarlo en cualquier momento en los ajustes del teléfono.
- [PRÓXIMA VERSIÓN · Firebase Analytics] Analítica de uso: [ABOGADO].

## Transferencias internacionales

RevenueCat y Google pueden tratar datos en Estados Unidos. Estas transferencias se basan
en [COMPLETAR/ABOGADO].

## Cuánto tiempo se conservan

- RevenueCat: [COMPLETAR] (los registros de compra pueden conservarse el tiempo que
  exija la normativa fiscal y contable).
- Firebase Crashlytics: [COMPLETAR].
- [PRÓXIMA VERSIÓN · Firebase Analytics] Firebase Analytics: [COMPLETAR].
- Datos en tu dispositivo: hasta que los borres o desinstales la app.

## Tus derechos

Puedes pedirnos acceder a tus datos, corregirlos o borrarlos, limitar u oponerte a su
tratamiento y recibir una copia (arts. 15 a 21 RGPD). Cuando el tratamiento se basa en tu
consentimiento, puedes retirarlo en cualquier momento. También puedes reclamar ante la
autoridad italiana de protección de datos (Garante per la protezione dei dati personali,
garanteprivacy.it) o ante la del país de la UE en el que vivas.

## Borrar tus datos {#delete}

- En el teléfono: desinstala iSIMILAR. Se borran el índice, los vectores y los ajustes de
  la app. Tus fotos no se tocan.
- En los proveedores: escribe a info@isimilar.app con el asunto "Borrar mis datos" y tu
  ID de usuario de iSIMILAR. Para copiarlo, abre Ajustes en la app y mantén pulsado el
  número de versión, al final. Borraremos los datos asociados a ese ID en RevenueCat y
  Firebase en un plazo de [COMPLETAR], salvo los registros de compra que debamos
  conservar por ley.
- Borrar tus datos no cancela la suscripción. Para cancelarla, usa los ajustes de
  suscripciones de App Store o Google Play.

## Menores

iSIMILAR no está dirigida a menores de [COMPLETAR/ABOGADO] años y no recogemos datos
suyos de forma consciente.

## Cambios

Si cambia el uso que la app hace de los datos, actualizaremos esta página y la fecha de
arriba antes de que el cambio llegue a la app.

## Contacto

info@isimilar.app
```

### 2.3 Informativa sulla privacy (IT)

```
# Informativa sulla privacy di iSIMILAR

Ultimo aggiornamento: [COMPLETAR]

iSIMILAR è un'app di ricerca visiva per le foto del tuo telefono. Questa informativa
spiega quali dati usa l'app, cosa esce dal dispositivo e quali sono i tuoi diritti.

## In breve

- Le tue foto non escono mai dal telefono. Le foto, le miniature e le "impronte" visive
  (vettori) calcolate dall'app vengono create e salvate solo sul tuo dispositivo.
- Non esistono account utente. Non ti chiediamo mai nome, email o numero di telefono.
- L'app invia un insieme limitato di dati tecnici su acquisti, utilizzo ed errori ai
  fornitori elencati sotto. Questi dati sono associati a un identificativo casuale, non al
  tuo nome. Ai sensi del Regolamento generale sulla protezione dei dati (GDPR) sono dati
  pseudonimi, non anonimi.
- Non usiamo i tuoi dati per la pubblicità, non ti tracciamo su altre app o siti, non
  raccogliamo l'identificativo pubblicitario (IDFA su iOS, ID pubblicità su Android) e non
  vendiamo i tuoi dati.

## Titolare del trattamento

Titolare: [COMPLETAR]
Indirizzo: [COMPLETAR]
P. IVA: [COMPLETAR]
Contatto privacy: info@isimilar.app

## Cosa resta sul tuo dispositivo

- Le tue foto e gli album che crei o modifichi.
- Le miniature (224 px) usate per analizzare le foto.
- I vettori (sequenze di numeri che descrivono l'aspetto di una foto) e l'indice di
  ricerca. Sono salvati in un database locale e vengono cancellati quando disinstalli
  l'app.
- Le foto che scatti con la fotocamera per cercare.

L'analisi visiva avviene interamente sul telefono, con o senza connessione. Niente di
tutto questo viene inviato a noi o a terzi.

## Cosa esce dal dispositivo e perché

| Servizio (fornitore) | Cosa riceve | Perché |
|---|---|---|
| RevenueCat (RevenueCat, Inc., USA) | Lo stato del tuo acquisto e abbonamento, un identificativo casuale creato da RevenueCat e questi campi di misurazione: cosa ha aperto la schermata di upgrade (fotocamera, eliminazione multipla, spostamento multiplo in un album, impostazioni), quante foto erano selezionate, la dimensione della galleria per fasce (meno di 3.000, da 3.000 a 10.000, oltre 10.000) e, se scegli di rispondere, per cosa usi l'app. | Gestire e ripristinare l'abbonamento e capire quali funzioni portano a passare a PRO. |
| Firebase Crashlytics (Google) | Report di arresti anomali e dati sulle prestazioni: dettagli tecnici dell'errore, versione dell'app, modello del dispositivo e versione del sistema operativo, associati a un identificativo di installazione. | Trovare e correggere gli errori. |
| Firebase Remote Config (Google) | Versione dell'app e del sistema operativo, paese e lingua impostati, associati a un identificativo di installazione. | Avvisarti quando un aggiornamento è obbligatorio. |
| Firebase Cloud Messaging (Google) | Un token per le notifiche del dispositivo, modello, lingua, fuso orario e versione del sistema operativo. Solo se consenti le notifiche. | Inviare notifiche. |
| [PROSSIMA VERSIONE · Firebase Analytics] Google Analytics per Firebase (Google) | Eventi di utilizzo: scansione avviata o completata (numero di foto e durata), ricerca dalla galleria o dalla fotocamera, azioni sulle foto (eliminare, spostare in un album, togliere da un album, condividere; numero di foto; se multipla), schermata di upgrade mostrata e risposta sull'utilizzo, associati a un identificativo dell'istanza dell'app. Nessuna foto, miniatura, vettore o contenuto delle immagini. La raccolta dell'identificativo pubblicitario è disattivata e i segnali pubblicitari sono negati. | Capire come viene usata l'app e migliorarla. |

Nessuno di questi servizi riceve le tue foto, miniature, vettori, nomi dei file, posizioni
salvate nelle foto o qualsiasi altro contenuto della galleria.

I pagamenti sono gestiti da Apple (App Store) o Google (Google Play). Non vediamo mai i
dati della tua carta o del tuo conto; riceviamo solo lo stato dell'acquisto tramite
RevenueCat.

Ogni fornitore tratta i dati per nostro conto in base a un accordo sul trattamento dei
dati ed è tenuto a proteggerli almeno al livello descritto in questa informativa.

## Autorizzazioni richieste

- Foto: per scansionare e cercare nella galleria sul dispositivo, e per eliminare,
  spostare o condividere foto quando lo confermi. Necessaria per il funzionamento.
- Fotocamera: per scattare una foto e usarla come ricerca. Facoltativa; la foto resta sul
  telefono.
- Notifiche: per il promemoria settimanale facoltativo e avvisi sull'app. Facoltative.

## Base giuridica (GDPR)

- Gestione dell'abbonamento: esecuzione di un contratto (art. 6, par. 1, lett. b GDPR).
- Report di errori, verifica degli aggiornamenti obbligatori e misurazione di cosa porta
  a passare a PRO: nostro legittimo interesse a far funzionare e migliorare l'app
  (art. 6, par. 1, lett. f).
- Notifiche: il tuo consenso, dato tramite la richiesta di autorizzazione del telefono
  (art. 6, par. 1, lett. a). Puoi revocarlo in qualsiasi momento dalle impostazioni.
- [PROSSIMA VERSIONE · Firebase Analytics] Analisi dell'utilizzo: [ABOGADO].

## Trasferimenti internazionali

RevenueCat e Google possono trattare dati negli Stati Uniti. Questi trasferimenti si
basano su [COMPLETAR/ABOGADO].

## Per quanto tempo conserviamo i dati

- RevenueCat: [COMPLETAR] (i dati degli acquisti possono essere conservati per il tempo
  richiesto dalla normativa fiscale e contabile).
- Firebase Crashlytics: [COMPLETAR].
- [PROSSIMA VERSIONE · Firebase Analytics] Firebase Analytics: [COMPLETAR].
- Dati sul dispositivo: finché non li elimini o disinstalli l'app.

## I tuoi diritti

Puoi chiederci di accedere ai tuoi dati, rettificarli o cancellarli, limitarne o opporti
al trattamento e riceverne una copia (artt. 15-21 GDPR). Se il trattamento si basa sul
consenso, puoi revocarlo in qualsiasi momento. Puoi anche proporre reclamo al Garante per
la protezione dei dati personali (garanteprivacy.it) o all'autorità del paese UE in cui
vivi.

## Cancellare i tuoi dati {#delete}

- Sul telefono: disinstalla iSIMILAR. Vengono cancellati l'indice, i vettori e le
  impostazioni dell'app. Le tue foto non vengono toccate.
- Presso i fornitori: scrivi a info@isimilar.app con oggetto "Cancella i miei dati" e il
  tuo ID utente iSIMILAR. Per copiarlo, apri Impostazioni nell'app e tieni premuto il
  numero di versione in fondo. Cancelleremo i dati associati a quell'ID in RevenueCat e
  Firebase entro [COMPLETAR], salvo i dati degli acquisti che dobbiamo conservare per
  legge.
- Cancellare i dati non annulla l'abbonamento. Per annullarlo, usa le impostazioni degli
  abbonamenti di App Store o Google Play.

## Minori

iSIMILAR non è rivolta a minori di [COMPLETAR/ABOGADO] anni e non raccogliamo
consapevolmente i loro dati.

## Modifiche

Se cambia il modo in cui l'app usa i dati, aggiorneremo questa pagina e la data in alto
prima che la modifica arrivi nell'app.

## Contatti

info@isimilar.app
```

### 2.4 Terms of Use (EN, versión principal)

```
# iSIMILAR Terms of Use

Last updated: [COMPLETAR]

These terms apply to the iSIMILAR app on iOS and Android. By using the app you accept
them. If you downloaded iSIMILAR from the App Store, Apple's Standard Licensed
Application End User License Agreement also applies.

Provider: [COMPLETAR: nombre o razón social, dirección, P. IVA] · info@isimilar.app

## What iSIMILAR does

iSIMILAR finds photos in your gallery that look like a photo you choose or take with the
camera. It compares shape, texture, colour and composition. It works on your phone,
without an internet connection, and your photos never leave the device.

Results are based on visual similarity, not on exact identification. The app may show
photos that are not related, and may miss photos that are. It does not search by text,
date, location or person, and it does not recognise faces or name objects.

## Free and PRO

Free: gallery scan, unlimited searches from saved photos, 5 searches with the camera, and
deleting photos one at a time.

iSIMILAR PRO: unlimited camera searches and batch actions (deleting or moving many photos
at once).

## Subscription, free trial and renewal

- iSIMILAR PRO is an auto-renewing annual subscription.
- Price: 12 € per year in the euro area and 11.99 USD per year in the United States; in
  other countries, the equivalent price set by the App Store or Google Play. The exact
  price, in your currency and including applicable taxes, is shown in the app before you
  confirm.
- Free trial: eligible new subscribers get 7 days free. If you do not cancel before the
  trial ends, the annual price is charged at the end of the trial and the subscription
  starts.
- Renewal: the subscription renews automatically every year at the then-current price
  unless you cancel before the end of the current period. [VERIFICAR: Apple indica que
  la renovación automática debe desactivarse al menos 24 horas antes del final del
  periodo; confirmar en la documentación de Apple antes de publicar esta frase.]
- Payment is charged to your Apple ID or Google account by Apple or Google. We do not
  process or store payment details.
- Manage or cancel: App Store › your name › Subscriptions
  (https://apps.apple.com/account/subscriptions), or Google Play › Payments &
  subscriptions › Subscriptions (https://play.google.com/store/account/subscriptions).
  Deleting the app does not cancel the subscription.
- After cancelling, you keep PRO until the end of the period you already paid for.
- Restore: if you change or reinstall your phone, use "Restore Purchases" in the app with
  the same Apple ID or Google account.

## Refunds

Refunds are handled by Apple or Google under their policies. [ABOGADO: derecho de
desistimiento de 14 días para contenido digital (Directiva 2011/83/UE) y cómo se aplica
cuando la compra la procesa la tienda.]

## Your photos and your decisions

You decide what to delete, move or share. The app always shows a preview and asks for
confirmation. Review results before confirming: a deleted photo may not be recoverable
from iSIMILAR. We recommend keeping a backup of photos that matter to you.

## Licence and acceptable use

We grant you a personal, non-exclusive, non-transferable licence to use iSIMILAR on
devices you own or control. Do not copy, modify, reverse engineer or resell the app
except where the law allows it.

## Privacy

How the app handles data is explained in the Privacy Policy: https://isimilar.app/privacy

## Liability

[ABOGADO: limitación de responsabilidad compatible con la normativa de consumo de la UE
e Italia (Codice del Consumo). No se puede excluir la responsabilidad por dolo, culpa
grave ni los derechos legales del consumidor.]

## Changes to these terms

We may update these terms. The date above shows the latest version. Important changes
will be announced in the app or on this page before they apply.

## Applicable law

[ABOGADO: ley italiana, sin perjuicio de las normas imperativas de protección del
consumidor del país de residencia del usuario.]

## Contact

info@isimilar.app
```

### 2.5 Términos de uso (ES)

```
# Términos de uso de iSIMILAR

Última actualización: [COMPLETAR]

Estos términos se aplican a la app iSIMILAR en iOS y Android. Al usarla los aceptas. Si
descargaste iSIMILAR desde la App Store, también se aplica el Contrato de Licencia de
Usuario Final estándar de Apple.

Proveedor: [COMPLETAR] · info@isimilar.app

## Qué hace iSIMILAR

iSIMILAR encuentra en tu galería las fotos que se parecen a una que eliges o que haces
con la cámara. Compara forma, textura, color y composición. Funciona en tu teléfono, sin
conexión a internet, y tus fotos nunca salen del dispositivo.

Los resultados se basan en el parecido visual, no en una identificación exacta. La app
puede mostrar fotos que no tienen relación y dejar fuera otras que sí la tienen. No busca
por texto, fecha, ubicación ni persona, y no reconoce caras ni nombra objetos.

## Gratis y PRO

Gratis: escaneo de la galería, búsquedas ilimitadas desde fotos guardadas, 5 búsquedas
con la cámara y borrado de fotos de una en una.

iSIMILAR PRO: búsquedas con cámara ilimitadas y acciones en lote (borrar o mover muchas
fotos a la vez).

## Suscripción, prueba gratuita y renovación

- iSIMILAR PRO es una suscripción anual de renovación automática.
- Precio: 12 € al año en la zona euro y 11,99 USD al año en Estados Unidos; en otros
  países, el equivalente que fija la App Store o Google Play. El precio exacto, en tu
  moneda y con los impuestos aplicables, se muestra en la app antes de confirmar.
- Prueba gratuita: los nuevos suscriptores que cumplan los requisitos tienen 7 días
  gratis. Si no cancelas antes de que termine la prueba, se cobra el precio anual al
  terminar y empieza la suscripción.
- Renovación: la suscripción se renueva automáticamente cada año al precio vigente salvo
  que la canceles antes del final del periodo en curso. [VERIFICAR: plazo de 24 horas de
  Apple.]
- El cobro lo hace Apple o Google en tu Apple ID o cuenta de Google. No tratamos ni
  guardamos datos de pago.
- Gestionar o cancelar: App Store › tu nombre › Suscripciones
  (https://apps.apple.com/account/subscriptions), o Google Play › Pagos y suscripciones ›
  Suscripciones (https://play.google.com/store/account/subscriptions). Borrar la app no
  cancela la suscripción.
- Tras cancelar, mantienes PRO hasta el final del periodo ya pagado.
- Restaurar: si cambias de teléfono o reinstalas, usa "Restaurar compras" en la app con
  el mismo Apple ID o cuenta de Google.

## Reembolsos

Los reembolsos los gestiona Apple o Google según sus políticas. [ABOGADO: derecho de
desistimiento.]

## Tus fotos y tus decisiones

Tú decides qué borrar, mover o compartir. La app siempre muestra una vista previa y pide
confirmación. Revisa los resultados antes de confirmar: una foto borrada puede no ser
recuperable desde iSIMILAR. Te recomendamos tener copia de las fotos importantes.

## Licencia y uso aceptable

Te concedemos una licencia personal, no exclusiva e intransferible para usar iSIMILAR en
dispositivos que sean tuyos o que controles. No copies, modifiques, descompiles ni
revendas la app salvo donde la ley lo permita.

## Privacidad

Cómo trata la app los datos se explica en la Política de privacidad:
https://isimilar.app/es/privacy

## Responsabilidad

[ABOGADO]

## Cambios en estos términos

Podemos actualizar estos términos. La fecha de arriba indica la última versión. Los
cambios importantes se anunciarán en la app o en esta página antes de aplicarse.

## Ley aplicable

[ABOGADO]

## Contacto

info@isimilar.app
```

### 2.6 Termini d'uso (IT)

```
# Termini d'uso di iSIMILAR

Ultimo aggiornamento: [COMPLETAR]

Questi termini si applicano all'app iSIMILAR su iOS e Android. Usando l'app li accetti.
Se hai scaricato iSIMILAR dall'App Store, si applica anche il Contratto di licenza
standard per l'utente finale di Apple.

Fornitore: [COMPLETAR] · info@isimilar.app

## Cosa fa iSIMILAR

iSIMILAR trova nella tua galleria le foto che somigliano a una foto che scegli o che
scatti con la fotocamera. Confronta forma, texture, colore e composizione. Funziona sul
telefono, senza connessione a internet, e le tue foto non escono mai dal dispositivo.

I risultati si basano sulla somiglianza visiva, non su un'identificazione esatta. L'app
può mostrare foto non correlate e non trovarne altre che lo sono. Non cerca per testo,
data, luogo o persona, non riconosce volti e non dà un nome agli oggetti.

## Gratis e PRO

Gratis: scansione della galleria, ricerche illimitate da foto salvate, 5 ricerche con la
fotocamera ed eliminazione delle foto una alla volta.

iSIMILAR PRO: ricerche con fotocamera illimitate e azioni multiple (eliminare o spostare
molte foto insieme).

## Abbonamento, prova gratuita e rinnovo

- iSIMILAR PRO è un abbonamento annuale a rinnovo automatico.
- Prezzo: 12 € all'anno nell'area euro e 11,99 USD all'anno negli Stati Uniti; negli
  altri paesi, l'equivalente stabilito dall'App Store o da Google Play. Il prezzo esatto,
  nella tua valuta e con le imposte applicabili, è mostrato nell'app prima della conferma.
- Prova gratuita: i nuovi abbonati idonei hanno 7 giorni gratis. Se non annulli prima
  della fine della prova, al termine viene addebitato il prezzo annuale e l'abbonamento
  inizia.
- Rinnovo: l'abbonamento si rinnova automaticamente ogni anno al prezzo in vigore, salvo
  annullamento prima della fine del periodo in corso. [VERIFICAR: termine di 24 ore di
  Apple.]
- L'addebito è effettuato da Apple o Google sul tuo ID Apple o account Google. Non
  trattiamo né conserviamo dati di pagamento.
- Gestire o annullare: App Store › il tuo nome › Abbonamenti
  (https://apps.apple.com/account/subscriptions), oppure Google Play › Pagamenti e
  abbonamenti › Abbonamenti (https://play.google.com/store/account/subscriptions).
  Eliminare l'app non annulla l'abbonamento.
- Dopo l'annullamento, mantieni PRO fino alla fine del periodo già pagato.
- Ripristino: se cambi telefono o reinstalli l'app, usa "Ripristina acquisti" con lo
  stesso ID Apple o account Google.

## Rimborsi

I rimborsi sono gestiti da Apple o Google secondo le loro politiche. [ABOGADO: diritto
di recesso.]

## Le tue foto e le tue decisioni

Sei tu a decidere cosa eliminare, spostare o condividere. L'app mostra sempre
un'anteprima e chiede conferma. Controlla i risultati prima di confermare: una foto
eliminata potrebbe non essere recuperabile da iSIMILAR. Ti consigliamo di avere un backup
delle foto importanti.

## Licenza e uso consentito

Ti concediamo una licenza personale, non esclusiva e non trasferibile per usare iSIMILAR
su dispositivi di tua proprietà o sotto il tuo controllo. Non copiare, modificare,
decompilare o rivendere l'app, salvo quando la legge lo consente.

## Privacy

Il trattamento dei dati è spiegato nell'Informativa sulla privacy:
https://isimilar.app/it/privacy

## Responsabilità

[ABOGADO]

## Modifiche ai termini

Possiamo aggiornare questi termini. La data in alto indica l'ultima versione. Le
modifiche importanti saranno comunicate nell'app o in questa pagina prima di entrare in
vigore.

## Legge applicabile

[ABOGADO]

## Contatti

info@isimilar.app
```

### 2.7 Qué cambia cuando llegue Firebase Analytics (y qué se actualiza el mismo día)

`definicion-tecnica.md` · "Datos y privacidad" obliga a actualizar a la vez política, etiqueta de la
App Store y formulario de Google Play. Lista concreta:

| Pieza | Cambio | Estado hoy |
|---|---|---|
| `/privacy` (EN/ES/IT) | Publicar la fila "Firebase Analytics", su base jurídica, su plazo de conservación y la fecha nueva. | Texto preparado arriba, marcado [NEXT VERSION]. |
| Base jurídica / consentimiento | Decidir interés legítimo o pantalla de consentimiento (ePrivacy art. 5(3); Codice privacy art. 122). Si es consentimiento, hace falta cambiar la app antes de publicar. | **[ABOGADO]** · bloqueante. |
| Etiqueta App Store (App Store Connect › App Privacy) | Revisar con la guía de declaración de Firebase: Analytics usa un ID de instancia de la app (Device ID) y eventos de interacción (Product Interaction). La etiqueta actual ya declara ambos tipos; hay que comprobar que el propósito "Analytics" está marcado para cada uno y resolver C4 (vinculados / no vinculados). Comprobar también si Analytics deriva ubicación aproximada de la IP: **no puedo confirmarlo** con la documentación de Firebase que he leído. Se puede cambiar sin enviar versión nueva (Apple, App Privacy Details). | Sin verificar. |
| Google Play › Contenido de la app › Seguridad de los datos | Añadir o confirmar: "Interacciones con la app" (Analytics), "ID de dispositivo u otros" (Analytics, funcionalidad), "Registros de fallos" y "Diagnóstico" (Crashlytics), "Historial de compras" (RevenueCat). Indicar que no se comparten con fines publicitarios y cómo pedir el borrado (`/privacy#delete`). Google: "Your Data safety form responses must remain accurate and complete at all times." | Sin verificar (no veo la consola). |
| Atributos/eventos | El valor `remove_album` existe en el código y no en el documento: si se publica, la política ya lo menciona ("remove from album"). | Ver nota en 1.C. |
| Fecha de la política | Cambiar "Last updated" en los 3 idiomas. | — |

---

## 3. Plan de migración Notion → isimilar.app

### 3.1 Por qué no borrar Notion hasta el final
1. **Las versiones instaladas llevan las URL de Notion escritas en el código** (`premium_offer_sheet.dart:896, 916`; `settings_view.dart:652, 658, 664`). Quien no actualice seguirá abriendo Notion: si se borra, el enlace de privacidad del muro de pago queda roto.
2. **Apple exige el enlace de privacidad dentro de la app** (5.1.1(i)) y los términos/privacidad en el flujo de suscripción. Un revisor que abra un enlace roto puede rechazar la siguiente versión.
3. **Google exige una URL activa y accesible** (User Data › Privacy Policy). Un enlace muerto en Play Console puede acabar en aviso o retirada.
4. **Rendición de cuentas (RGPD art. 5.2):** conviene conservar la versión antigua como prueba de qué se informaba y cuándo.

### 3.2 Orden recomendado
| Paso | Qué | Dónde | Nota |
|---|---|---|---|
| 0 | Exportar a Markdown el texto actual de las 3 páginas de Notion (privacidad, términos, borrado de datos) y guardarlo en `archivo/` con fecha. | Notion | Resuelve también la auditoría 1.B. |
| 1 | Resolver C1-C6, completar los [COMPLETAR] y pasar los [ABOGADO]. | `borradores/` | Bloqueante para publicar. |
| 2 | Publicar `/privacy`, `/terms` (+ `/es/…`, `/it/…`) y comprobar que cargan sin JavaScript, en HTTPS, sin geobloqueo. | Web (Fase 2-3) | `checklist-release`. |
| 3 | App Store Connect › App Information › Privacy Policy URL → `https://isimilar.app/privacy` (y por idioma si se localiza). | App Store Connect | No requiere versión nueva. |
| 4 | App Store Connect: enlace a Terms of Use en la descripción de cada idioma o en el campo de EULA. | App Store Connect | Apple: "App Store metadata must include links to your Terms of Use and Privacy Policy". |
| 5 | Play Console › Política › Contenido de la app › Política de privacidad → `https://isimilar.app/privacy`. Si el formulario de seguridad de datos enlaza a una página de borrado, cambiarla a `/privacy#delete`. | Play Console | — |
| 6 | Descripción de la ficha en ambas tiendas (si menciona enlaces) y biografías/perfiles que enlacen a Notion. | Tiendas, redes | Revisar con `growth`. |
| 7 | App: sustituir las 5 URL de Notion por `/privacy`, `/terms` y `/privacy#delete` (mejor según idioma del teléfono). Publicar versión. | Sesión en `solopila/` | Aprovechar para C3 y C5. |
| 8 | Cuando la mayoría haya actualizado (o tras forzar la actualización con Remote Config, que ya existe en `force_update_service.dart`), sustituir el contenido de cada página de Notion por: "This policy has moved to https://isimilar.app/privacy" (y equivalente para términos y borrado). **No borrar las páginas.** | Notion | Mantener indefinidamente; no cuesta nada. |

**Detalle a verificar:** las URL de Notion que hay en la app no son idénticas a las que me pasaste
(app: `Privacy-Policy-for-iSimilar-…`, `Terms-and-Conditions-13d88278a02e80e4b5f8d790f9d388f1`; tú:
`Privacy-Policy-for-iSIMILAR-…`, `Terms-and-Conditions-for-iSIMILAR-…`). El identificador final coincide
y Notion suele resolver por él, pero **no puedo confirmar** que ambas variantes abran la página: compruébalo
en un navegador.

---

## 4. Fuentes oficiales consultadas (2026-10-21)
- Apple App Review Guidelines, 3.1.1, 3.1.2(a), 3.1.2(c), 5.1.1(i), 5.1.1(iii), 5.1.2(i): https://developer.apple.com/app-store/review/guidelines/
- Apple, Auto-renewable subscriptions ("Clearly describing subscriptions", "Billing amount", "Free trials"): https://developer.apple.com/app-store/subscriptions/
- Apple, App Privacy Details: https://developer.apple.com/app-store/app-privacy-details/
- Google Play, User Data › Privacy Policy: https://support.google.com/googleplay/android-developer/answer/10144311
- Google Play, Data safety: https://support.google.com/googleplay/android-developer/answer/10787469
- Google Play, política de suscripciones: https://support.google.com/googleplay/android-developer/answer/9900533
- Firebase, datos para la App Store: https://firebase.google.com/docs/ios/app-store-data-collection
- EDPB Guidelines 2/2023 (v2.0, 16-10-2024; no leído el PDF): https://www.edpb.europa.eu/documents/530_en
- RevenueCat DPA: https://www.revenuecat.com/dpa
- No pude leer el Anexo/Schedule 2 del Apple Developer Program License Agreement (texto demasiado largo y truncado).
