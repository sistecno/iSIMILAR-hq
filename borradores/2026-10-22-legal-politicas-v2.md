# iSIMILAR · Textos legales v2: privacidad, términos, borrado de datos y etiquetas de tienda

Fecha: 2026-10-22 · Autor: legal-tiendas · Estado: BORRADOR, no publicar sin resolver los marcadores.
Sustituye por completo a: `archivo/Privacy_Policy_for_iSIMILAR.md`, `archivo/Terms-and-Conditions-iSIMILAR.md`,
`archivo/Data_Deletion_iSimilar.md` y a las secciones 2.1-2.7 de `borradores/web-fase1-legal.md`.

> **Aviso:** no es asesoramiento legal definitivo. Lo he redactado a partir de los documentos de `docs/`,
> del código de `solopila/` y de la documentación oficial de Apple, Google, Firebase y RevenueCat
> consultada el 22-10-2026. Los puntos **[ABOGADO]** necesitan revisión de un abogado de protección
> de datos y consumo en Italia antes de publicar.

**Marcadores**
- `[NOMBRE COMPLETO]`, `[DIRECCIÓN]`, `[P. IVA]`, `[EMAIL DE CONTACTO]`: datos del responsable.
  Sugerencia para `[EMAIL DE CONTACTO]`: **info@isimilar.app** [CONFIRMAR: el buzón debe existir y
  revisarse; el RGPD da un mes para responder]. `info@creadoresdeventas.com` ya no se usa.
- `[FECHA DE PUBLICACIÓN]`: la fecha del día en que se publique.
- `[VERIFICAR]`: dato que no he podido confirmar en una fuente oficial.
- `[DECIDIR]`: decisión de Anibal (plazos, opciones).
- `[ABOGADO]`: necesita revisión legal (lista en el apartado 5).
- Ningún texto se publica con corchetes.

---

## 0. Lo más urgente (riesgo de rechazo o de sanción, primero)

| # | Requisito | Estado | Evidencia | Acción |
|---|---|---|---|---|
| 1 | La app no envía datos que la política no declare (RGPD art. 13; Apple 5.1.1(i); Google Play, Datos del usuario) | **No cumple si se publica el código actual** | `solopila/pubspec.yaml:51` sigue incluyendo `firebase_analytics`; `lib/main.dart:22` llama a `AnalyticsService.init()`; `analytics_service.dart:184` envía eventos. Con el SDK dentro, Firebase Analytics también recoge eventos automáticos aunque los métodos estén vacíos. | Quitar la dependencia y las llamadas antes de compilar (ver C1). Bloqueante. |
| 2 | Consentimiento para leer o enviar información del teléfono que no es estrictamente necesaria (Directiva ePrivacy art. 5.3; en Italia, art. 122 del Codice privacy) | **Sin verificar: riesgo legal real** | El problema que ha sacado a Firebase Analytics de la versión también afecta a los atributos de medición de RevenueCat: `gallery_size` sale del número de fotos de la galería y `paywall_trigger` y `batch_size` describen el uso. No son necesarios para cobrar. Lo mismo vale, en menor grado, para Crashlytics y para el token de Cloud Messaging, que se crea al arrancar la app y no al dar permiso. | **[ABOGADO]** antes de publicar (apartado 5, punto 1). No reabro la decisión de enviar los atributos: aviso de que puede necesitar el mismo tratamiento que Analytics. |
| 3 | La etiqueta de la App Store es exacta | **No cumple (probable)** | Apple (App Privacy Details): *"'Personal Information' and 'Personal Data', as defined under relevant privacy laws, are considered linked to the user."* Los datos seudónimos son datos personales según el RGPD (considerando 26). | Declarar "vinculados" (apartado 4.1). Ver C2. Se cambia en App Store Connect sin enviar versión nueva. |
| 4 | El precio que se muestra antes de pagar es el que se cobra (Apple, Auto-renewable subscriptions, "Billing amount"; Google Play, política de suscripciones) | **No cumple en un caso concreto** | `premium_service.dart:84-85` y `:90-91` muestran `$12.99` si la tienda no devuelve el precio. El precio real en EE. UU. es 11,99 USD. | Ver C3. |
| 5 | Política, términos y borrado accesibles desde la app y la ficha (Apple 5.1.1(i) y página de suscripciones: *"your app and App Store metadata must include links to your Terms of Use and Privacy Policy"*) | **Cumple en la app, con contenido desfasado** | Enlaces a Notion en `premium_offer_sheet.dart:896, 916` y `settings_view.dart:652, 658, 664`. El texto de Notion habla de créditos, de "anonymous crash reports", de notificaciones promocionales y de la ley española. | Sustituir el contenido de las 3 páginas de Notion por estos textos el mismo día en que se publique la web, o antes. |
| 6 | Identificación del responsable (RGPD art. 13.1.a; P. IVA en la web según el DPR 633/1972, art. 35) | **No cumple** | Los textos de Notion citan "Creadores de Ventas" y un correo que ya no corresponde. La web no enlaza ni la política ni los términos. | Rellenar los datos (apartado 1.0). |

---

## 1. Política de privacidad

### 1.0 Datos del responsable: qué es obligatorio en la web

| Dato | ¿Obligatorio? | Fuente | Dónde |
|---|---|---|---|
| Nombre completo (`[NOMBRE COMPLETO]`) | **Sí** | RGPD art. 13.1.a ("identidad y datos de contacto del responsable"); D.Lgs. 70/2003 art. 7 | Política, términos y pie de la web |
| Correo de contacto (`[EMAIL DE CONTACTO]`) | **Sí** | RGPD art. 13.1.a; D.Lgs. 70/2003 art. 7 (contacto rápido, incluido el correo) | Política, términos y página de borrado |
| P. IVA (`[P. IVA]`) | **Sí, en la página de inicio de la web** | DPR 633/1972, art. 35 (resolución 60/E de 2006 de la Agenzia delle Entrate: también si la web solo sirve de escaparate) | Pie de todas las páginas de isimilar.app y en la política |
| Dirección (`[DIRECCIÓN]`) | **Sí** en la práctica | D.Lgs. 70/2003 art. 7 (domicilio o sede); Codice del Consumo art. 49 (dirección geográfica antes de un contrato a distancia) | Política y términos. **[ABOGADO]**: si puede ser un domicilio profesional en lugar del de residencia |
| Número REA o de inscripción en el Registro delle Imprese | **Solo si estás inscrito** (empresa individual). Un profesional autónomo sin inscripción no lo tiene | D.Lgs. 70/2003 art. 7 | **[ABOGADO / commercialista]** |
| Teléfono | Opcional (el Codice del Consumo lo pide "si está disponible") | Codice del Consumo art. 49 | Recuerda que la App Store ya muestra en la UE los datos de "comerciante" de la Ley de Servicios Digitales: deben coincidir |
| PEC | Opcional en la web | — | — |
| Delegado de protección de datos | No es obligatorio para esta actividad | RGPD art. 37 | La política dice que no hay |

**Comprobar** [VERIFICAR]: que el nombre del vendedor en App Store Connect, el del desarrollador en Google Play
Console y los datos de "comerciante" de la UE coinciden con `[NOMBRE COMPLETO]` y `[P. IVA]`. Si la cuenta
de desarrollador está a nombre de otra persona o empresa, el responsable del tratamiento declarado no
coincidirá con quien vende la app.

### 1.1 Privacy Policy (EN)

```
# iSIMILAR Privacy Policy

Last updated: [FECHA DE PUBLICACIÓN]

This policy explains what data the iSIMILAR app uses, what leaves your phone and why,
and what rights you have. It applies to the iSIMILAR app for iOS and Android.

## 1. The short version

- Your photos never leave your phone. Your photos, the thumbnails used to analyse them
  and the visual vectors the app calculates are created, stored and searched only on
  your device.
- There is no account. We never ask for your name, email address or phone number.
- To sell and manage the subscription, fix errors, deliver notifications and check for
  required updates, the app sends technical data about purchases, usage and errors to
  the service providers listed in section 5. This data never includes your photos or
  the content of your gallery.
- That data is linked to random identifiers, not to your name. Under the EU General Data
  Protection Regulation (GDPR) it is pseudonymous personal data, not anonymous data, and
  this policy treats it as personal data.
- We do not show ads, we do not track you across other companies' apps or websites, we do
  not collect the advertising identifier (IDFA on iOS, Advertising ID on Android) and we
  do not sell your data.

## 2. Who is responsible for your data

Data controller: [NOMBRE COMPLETO], sole trader established in Italy
Address: [DIRECCIÓN]
VAT number (P. IVA): [P. IVA]
Email: [EMAIL DE CONTACTO]

We have not appointed a Data Protection Officer because the law does not require one for
this activity. For any privacy question or request, write to the email above.

## 3. What stays on your phone

- Your photos and your albums.
- 224-pixel thumbnails the app creates temporarily to analyse each photo.
- The visual vectors (lists of numbers that describe what a photo looks like) and the
  search index, stored in a local database on your phone.
- The photo you take with the camera to search.
- Your app settings, such as language and notification preferences.

The visual analysis runs entirely on your phone and works without an internet
connection. None of this is sent to us or to anyone else. It is deleted when you use
Settings > Reset App or when you uninstall the app (see section 11).

## 4. Permissions the app asks for

- Photos: required. To scan and search your gallery on your phone and, only when you
  confirm it, to delete, move or share photos.
- Camera: optional. To take a photo and use it as a search.
- Notifications: optional. See section 6.

You can change these permissions at any time in your phone's settings.

## 5. What leaves your phone, and why

The app uses these service providers. Each one acts on our behalf as a data processor
under a data processing agreement and must protect your data at least to the level
described in this policy.

### RevenueCat (RevenueCat, Inc., United States): purchases and subscription

What it receives:
- Your purchase and subscription information: product, dates, price, currency, store,
  trial and renewal status.
- A random user ID created by RevenueCat when you first open the app. It is not your
  name, email or Apple or Google account.
- Basic technical data: app version, operating system, and language and region
  settings.
- These measurement fields:
  - paywall_trigger: what opened the PRO screen (a camera search, a batch delete, a
    batch move to an album, or the button in Settings).
  - batch_size: how many photos you had selected when the PRO screen opened from a batch
    action.
  - gallery_size: the size of your gallery as a range (under 3,000, 3,000 to 10,000, or
    over 10,000 photos). Sent once, after the first scan.
  - use_case: only if you choose to answer the optional question shown after a purchase
    or after a free trial starts: what you mainly use iSIMILAR for (repair and technical
    service; construction, installations or inspections; a portfolio; another type of
    work; cleaning up memes and screenshots; products, shopping and everyday photos; or
    something else). You can skip it.

Why: to process, validate and restore your subscription, and to understand which
features lead people to choose PRO and what they use the app for.

### Firebase Crashlytics (Google): error reports

What it receives: crash and error reports (technical details of the error and the state
of the app when it happened), device model, operating system version and app version,
linked to an installation identifier.

Why: to find and fix errors.

### Firebase Remote Config (Google): required updates

What it receives: country and language settings, time zone, operating system version and
app identifiers, linked to a Firebase installation identifier.

Why: to know the minimum app version that still works and, if yours is older, to ask you
to update.

### Firebase Cloud Messaging (Google): notifications

What it receives: a notification token linked to a Firebase installation identifier,
device model, language, time zone, operating system version and app version. The token
is created when the app starts; notifications are only shown if you allow them.

Why: to deliver notices about the app and about new versions (see section 6).

### What none of these providers receives

Your photos, thumbnails, vectors, the photo you take with the camera, or any other
content of your gallery.

### Payments

Payments are processed by Apple (App Store) or Google (Google Play) under their own terms
and privacy policies. We never see your card or bank details; we only receive the status
of your purchase through RevenueCat.

## 6. Notifications

iSIMILAR only sends:
- an optional weekly reminder to review your new photos, which you turn on in the app.
  It is created on your phone and sends no data;
- notices about the app and about new versions, through Firebase Cloud Messaging.

We do not send promotional or advertising notifications. You can turn notifications off
at any time in your phone's settings, and the weekly reminder in the app's Settings.

## 7. Legal basis (GDPR)

- Selling, validating and restoring your subscription: performance of a contract
  (Art. 6(1)(b) GDPR).
- Error reports and checking for required updates: our legitimate interest in keeping
  the app working and secure (Art. 6(1)(f)).
- The measurement fields paywall_trigger, batch_size and gallery_size: our legitimate
  interest in understanding which features lead people to choose PRO, using a small set
  of data that never includes your photos (Art. 6(1)(f)). [ABOGADO]
- Your answer to the optional use_case question: your consent, given by choosing to
  answer (Art. 6(1)(a)). You can withdraw it at any time by asking us to delete it.
  [ABOGADO]
- Notifications: your consent, given through your phone's permission prompt
  (Art. 6(1)(a)); the notification token is needed to deliver the notices you allow
  (Art. 6(1)(f)). [ABOGADO]
- Replying to your emails and requests: our legitimate interest in answering you and,
  for privacy requests, our legal obligation (Art. 6(1)(f) and 6(1)(c)).

Where we rely on legitimate interest, you have the right to object (section 10).

## 8. International transfers

RevenueCat and Google may process data in the United States.
- RevenueCat, Inc.: the European Commission's Standard Contractual Clauses, included in
  RevenueCat's data processing agreement.
- Google LLC (Firebase): Google is certified under the EU-U.S. Data Privacy Framework;
  Firebase's terms also include the Standard Contractual Clauses.

These providers use their own sub-processors, bound by the same obligations. You can ask
us for a copy of the safeguards. [ABOGADO]

## 9. How long we keep data

- Data on your phone: until you use Settings > Reset App or uninstall the app.
- Error reports (Crashlytics): 90 days; Google then starts removing them from its
  systems.
- Firebase installation identifiers (Remote Config, Cloud Messaging): until they are
  deleted; once deleted, Google removes them from its systems within 180 days.
  [VERIFICAR]
- Purchase data and measurement fields (RevenueCat): while your subscription is active
  and for [PLAZO: propuesta, 3 años desde tu última actividad] afterwards, or until you
  ask us to delete them. [DECIDIR] [ABOGADO]
- Emails you send us: [PLAZO: propuesta, 24 meses desde el último mensaje]. [DECIDIR]

Apple and Google keep their own records of your purchases under their own policies.

## 10. Your rights

You can ask us to access your data, correct it, delete it, restrict its processing,
receive a copy of it, and object to processing based on legitimate interest
(Arts. 15 to 21 GDPR). If processing is based on consent, you can withdraw it at any time
without affecting what was done before.

Because there is no account, we need your iSIMILAR ID to find your data in RevenueCat
(see section 11). Error reports and Firebase identifiers are not linked to that ID, so we
cannot identify which of them are yours (Art. 11 GDPR); the retention periods in section
9 still apply to them.

We will answer within one month. You can also lodge a complaint with the Italian data
protection authority, the Garante per la protezione dei dati personali
(www.garanteprivacy.it), or with the authority of the EU country where you live or work.

## 11. Deleting your data

You can delete the data on your phone at any time and ask us to delete the data held by
our providers. Step-by-step instructions: [URL DE LA PÁGINA DE BORRADO]

Deleting your data does not cancel your subscription. To cancel it, see the Terms of Use.

## 12. Age

You must be at least 14 years old, or the minimum age required by the laws of your
country if higher, to use iSIMILAR.

We do not knowingly collect data from anyone below that age. If you think this has
happened, write to us and we will delete it.

## 13. Automated decisions

We do not make decisions about you based solely on automated processing, and we do not
build advertising profiles.

## 14. Changes to this policy

If we change how the app uses data, we will update this page and the date above before
the change reaches the app. If the change is significant, we will also tell you in the
app.

## 15. Contact

[EMAIL DE CONTACTO]
```

### 1.2 Política de privacidad (ES)

```
# Política de privacidad de iSIMILAR

Última actualización: [FECHA DE PUBLICACIÓN]

Esta política explica qué datos usa la app iSIMILAR, qué sale de tu teléfono y para qué,
y qué derechos tienes. Se aplica a la app iSIMILAR para iOS y Android.

## 1. En resumen

- Tus fotos nunca salen del teléfono. Tus fotos, las miniaturas que se usan para
  analizarlas y los vectores visuales que calcula la app se crean, se guardan y se buscan
  solo en tu dispositivo.
- No hay cuentas. Nunca te pedimos nombre, correo ni teléfono.
- Para vender y gestionar la suscripción, corregir errores, enviar notificaciones y
  comprobar si hace falta actualizar, la app envía datos técnicos de compras, uso y
  errores a los proveedores del apartado 5. Esos datos nunca incluyen tus fotos ni el
  contenido de tu galería.
- Esos datos van asociados a identificadores aleatorios, no a tu nombre. Según el
  Reglamento General de Protección de Datos (RGPD) son datos personales seudónimos, no
  anónimos, y esta política los trata como datos personales.
- No mostramos publicidad, no te rastreamos en apps ni webs de otras empresas, no
  recogemos el identificador publicitario (IDFA en iOS, ID de publicidad en Android) y no
  vendemos tus datos.

## 2. Responsable de tus datos

Responsable del tratamiento: [NOMBRE COMPLETO], trabajador autónomo establecido en Italia
Dirección: [DIRECCIÓN]
P. IVA: [P. IVA]
Correo: [EMAIL DE CONTACTO]

No hemos designado un delegado de protección de datos porque la ley no lo exige para esta
actividad. Para cualquier pregunta o solicitud sobre privacidad, escribe al correo
indicado.

## 3. Qué se queda en tu teléfono

- Tus fotos y tus álbumes.
- Las miniaturas de 224 píxeles que la app crea de forma temporal para analizar cada foto.
- Los vectores visuales (listas de números que describen cómo es una foto) y el índice de
  búsqueda, guardados en una base de datos local de tu teléfono.
- La foto que haces con la cámara para buscar.
- Los ajustes de la app, como el idioma y las preferencias de notificaciones.

El análisis visual se hace por completo en tu teléfono y funciona sin conexión a internet.
Nada de esto se envía a nosotros ni a nadie. Se borra con Ajustes > Restablecer App o al
desinstalar la app (ver apartado 11).

## 4. Permisos que pide la app

- Fotos: necesario. Para escanear y buscar en tu galería dentro del teléfono y, solo
  cuando lo confirmas, para borrar, mover o compartir fotos.
- Cámara: opcional. Para hacer una foto y usarla como búsqueda.
- Notificaciones: opcional. Ver apartado 6.

Puedes cambiar estos permisos cuando quieras en los ajustes del teléfono.

## 5. Qué sale de tu teléfono y para qué

La app usa estos proveedores. Cada uno actúa por cuenta nuestra como encargado del
tratamiento, con un contrato de encargo, y debe proteger tus datos al menos con el nivel
que describe esta política.

### RevenueCat (RevenueCat, Inc., Estados Unidos): compras y suscripción

Qué recibe:
- La información de tu compra y tu suscripción: producto, fechas, precio, moneda, tienda
  y estado de la prueba y de la renovación.
- Un identificador de usuario aleatorio que RevenueCat crea la primera vez que abres la
  app. No es tu nombre, tu correo ni tu cuenta de Apple o Google.
- Datos técnicos básicos: versión de la app, sistema operativo y ajustes de idioma y
  región.
- Estos campos de medición:
  - paywall_trigger: qué abrió la pantalla de PRO (una búsqueda con la cámara, un borrado
    en lote, mover en lote a un álbum o el botón de Ajustes).
  - batch_size: cuántas fotos tenías seleccionadas cuando la pantalla de PRO se abrió
    desde una acción en lote.
  - gallery_size: el tamaño de tu galería por tramos (menos de 3.000, de 3.000 a 10.000 o
    más de 10.000 fotos). Se envía una sola vez, tras el primer escaneo.
  - use_case: solo si decides responder a la pregunta opcional que aparece después de una
    compra o del inicio de una prueba gratuita: para qué usas sobre todo iSIMILAR
    (reparación y servicio técnico; obras, instalaciones o inspecciones; un portfolio;
    otro tipo de trabajo; limpiar memes y capturas; productos, compras y fotos del día a
    día; u otra cosa). Puedes omitirla.

Para qué: gestionar, validar y restaurar tu suscripción, y entender qué funciones llevan a
elegir PRO y para qué se usa la app.

### Firebase Crashlytics (Google): informes de errores

Qué recibe: informes de cierres y errores (detalles técnicos del error y estado de la app
en ese momento), modelo del dispositivo, versión del sistema operativo y versión de la
app, asociados a un identificador de instalación.

Para qué: encontrar y corregir errores.

### Firebase Remote Config (Google): actualizaciones obligatorias

Qué recibe: ajustes de país e idioma, zona horaria, versión del sistema operativo e
identificadores de la app, asociados a un identificador de instalación de Firebase.

Para qué: saber cuál es la versión mínima de la app que sigue funcionando y, si la tuya
es anterior, pedirte que actualices.

### Firebase Cloud Messaging (Google): notificaciones

Qué recibe: un token de notificaciones asociado a un identificador de instalación de
Firebase, modelo del dispositivo, idioma, zona horaria, versión del sistema operativo y
versión de la app. El token se crea al abrir la app; las notificaciones solo se muestran
si las permites.

Para qué: enviarte avisos sobre la app y sobre versiones nuevas (ver apartado 6).

### Lo que no recibe ninguno de estos proveedores

Tus fotos, las miniaturas, los vectores, la foto que haces con la cámara ni ningún otro
contenido de tu galería.

### Pagos

Los pagos los procesa Apple (App Store) o Google (Google Play) según sus propios términos
y políticas de privacidad. Nunca vemos los datos de tu tarjeta ni de tu banco; solo
recibimos el estado de tu compra a través de RevenueCat.

## 6. Notificaciones

iSIMILAR solo envía:
- un recordatorio semanal opcional para revisar tus fotos nuevas, que activas en la app.
  Se crea en tu teléfono y no envía ningún dato;
- avisos sobre la app y sobre versiones nuevas, a través de Firebase Cloud Messaging.

No enviamos notificaciones promocionales ni publicitarias. Puedes desactivar las
notificaciones cuando quieras en los ajustes del teléfono, y el recordatorio semanal en
los Ajustes de la app.

## 7. Base jurídica (RGPD)

- Vender, validar y restaurar tu suscripción: ejecución de un contrato (art. 6.1.b RGPD).
- Informes de errores y comprobación de actualizaciones obligatorias: nuestro interés
  legítimo en que la app funcione y sea segura (art. 6.1.f).
- Los campos de medición paywall_trigger, batch_size y gallery_size: nuestro interés
  legítimo en entender qué funciones llevan a elegir PRO, con un conjunto pequeño de datos
  que nunca incluye tus fotos (art. 6.1.f). [ABOGADO]
- Tu respuesta a la pregunta opcional use_case: tu consentimiento, que das al decidir
  responder (art. 6.1.a). Puedes retirarlo cuando quieras pidiéndonos que la borremos.
  [ABOGADO]
- Notificaciones: tu consentimiento, que das en el aviso de permisos del teléfono
  (art. 6.1.a); el token de notificaciones es necesario para enviarte los avisos que
  permites (art. 6.1.f). [ABOGADO]
- Responder a tus correos y solicitudes: nuestro interés legítimo en atenderte y, en las
  solicitudes de privacidad, una obligación legal (arts. 6.1.f y 6.1.c).

Cuando la base es el interés legítimo, tienes derecho a oponerte (apartado 10).

## 8. Transferencias internacionales

RevenueCat y Google pueden tratar datos en Estados Unidos.
- RevenueCat, Inc.: cláusulas contractuales tipo de la Comisión Europea, incluidas en su
  contrato de encargo del tratamiento.
- Google LLC (Firebase): Google está certificada en el Marco de Privacidad de Datos
  UE-EE. UU.; los términos de Firebase incluyen también las cláusulas contractuales tipo.

Estos proveedores usan a su vez subencargados sujetos a las mismas obligaciones. Puedes
pedirnos una copia de las garantías. [ABOGADO]

## 9. Cuánto tiempo conservamos los datos

- Datos en tu teléfono: hasta que uses Ajustes > Restablecer App o desinstales la app.
- Informes de errores (Crashlytics): 90 días; después Google empieza a borrarlos de sus
  sistemas.
- Identificadores de instalación de Firebase (Remote Config, Cloud Messaging): hasta que
  se borran; una vez borrados, Google los elimina de sus sistemas en un máximo de 180
  días. [VERIFICAR]
- Datos de compra y campos de medición (RevenueCat): mientras tu suscripción esté activa
  y durante [PLAZO: propuesta, 3 años desde tu última actividad] después, o hasta que nos
  pidas borrarlos. [DECIDIR] [ABOGADO]
- Correos que nos envías: [PLAZO: propuesta, 24 meses desde el último mensaje]. [DECIDIR]

Apple y Google conservan sus propios registros de tus compras según sus políticas.

## 10. Tus derechos

Puedes pedirnos acceder a tus datos, rectificarlos, borrarlos, limitar su tratamiento,
recibir una copia y oponerte al tratamiento basado en el interés legítimo (arts. 15 a 21
RGPD). Si el tratamiento se basa en el consentimiento, puedes retirarlo cuando quieras,
sin que afecte a lo hecho antes.

Como no hay cuentas, necesitamos tu ID de iSIMILAR para encontrar tus datos en RevenueCat
(ver apartado 11). Los informes de errores y los identificadores de Firebase no están
asociados a ese ID, así que no podemos saber cuáles son tuyos (art. 11 RGPD); aun así se
les aplican los plazos del apartado 9.

Te responderemos en el plazo de un mes. También puedes reclamar ante la autoridad italiana
de protección de datos, el Garante per la protezione dei dati personali
(www.garanteprivacy.it), o ante la autoridad del país de la UE en el que vivas o trabajes.

## 11. Borrar tus datos

Puedes borrar en cualquier momento los datos de tu teléfono y pedirnos que borremos los
que tienen nuestros proveedores. Instrucciones paso a paso: [URL DE LA PÁGINA DE BORRADO]

Borrar tus datos no cancela la suscripción. Para cancelarla, consulta los Términos de uso.

## 12. Edad

Debes tener al menos 14 años, o la edad mínima que exija la ley de tu país si es mayor,
para usar iSIMILAR.

No recogemos de forma consciente datos de nadie por debajo de esa edad. Si crees que ha
ocurrido, escríbenos y los borraremos.

## 13. Decisiones automatizadas

No tomamos decisiones sobre ti basadas únicamente en un tratamiento automatizado ni
creamos perfiles publicitarios.

## 14. Cambios en esta política

Si cambia el uso que la app hace de los datos, actualizaremos esta página y la fecha de
arriba antes de que el cambio llegue a la app. Si el cambio es importante, también te lo
diremos en la app.

## 15. Contacto

[EMAIL DE CONTACTO]
```

### 1.3 Informativa sulla privacy (IT)

```
# Informativa sulla privacy di iSIMILAR

Ultimo aggiornamento: [FECHA DE PUBLICACIÓN]

Questa informativa spiega quali dati usa l'app iSIMILAR, cosa esce dal tuo telefono e
perché, e quali diritti hai. Si applica all'app iSIMILAR per iOS e Android.

## 1. In breve

- Le tue foto non escono mai dal telefono. Le foto, le miniature usate per analizzarle e i
  vettori visivi calcolati dall'app vengono creati, salvati e cercati solo sul tuo
  dispositivo.
- Non esistono account. Non ti chiediamo mai nome, email o numero di telefono.
- Per vendere e gestire l'abbonamento, correggere gli errori, inviare notifiche e
  verificare se serve un aggiornamento, l'app invia dati tecnici su acquisti, utilizzo ed
  errori ai fornitori elencati nella sezione 5. Questi dati non includono mai le tue foto
  né il contenuto della galleria.
- Questi dati sono associati a identificativi casuali, non al tuo nome. Ai sensi del
  Regolamento generale sulla protezione dei dati (GDPR) sono dati personali pseudonimi,
  non anonimi, e questa informativa li tratta come dati personali.
- Non mostriamo pubblicità, non ti tracciamo su app o siti di altre aziende, non
  raccogliamo l'identificativo pubblicitario (IDFA su iOS, ID pubblicità su Android) e non
  vendiamo i tuoi dati.

## 2. Titolare del trattamento

Titolare: [NOMBRE COMPLETO], lavoratore autonomo stabilito in Italia
Indirizzo: [DIRECCIÓN]
P. IVA: [P. IVA]
Email: [EMAIL DE CONTACTO]

Non abbiamo designato un responsabile della protezione dei dati perché la legge non lo
richiede per questa attività. Per qualsiasi domanda o richiesta sulla privacy, scrivi
all'indirizzo indicato.

## 3. Cosa resta sul tuo telefono

- Le tue foto e i tuoi album.
- Le miniature da 224 pixel che l'app crea temporaneamente per analizzare ogni foto.
- I vettori visivi (sequenze di numeri che descrivono l'aspetto di una foto) e l'indice di
  ricerca, salvati in un database locale sul telefono.
- La foto che scatti con la fotocamera per cercare.
- Le impostazioni dell'app, come la lingua e le preferenze delle notifiche.

L'analisi visiva avviene interamente sul telefono e funziona senza connessione a internet.
Niente di tutto questo viene inviato a noi o ad altri. Viene cancellato con Impostazioni >
Reimposta App o disinstallando l'app (vedi sezione 11).

## 4. Autorizzazioni richieste dall'app

- Foto: necessaria. Per scansionare e cercare nella galleria sul telefono e, solo quando lo
  confermi, per eliminare, spostare o condividere foto.
- Fotocamera: facoltativa. Per scattare una foto e usarla come ricerca.
- Notifiche: facoltative. Vedi sezione 6.

Puoi modificare queste autorizzazioni in qualsiasi momento dalle impostazioni del telefono.

## 5. Cosa esce dal tuo telefono e perché

L'app usa questi fornitori. Ognuno agisce per nostro conto come responsabile del
trattamento, in base a un accordo sul trattamento dei dati, ed è tenuto a proteggere i tuoi
dati almeno al livello descritto in questa informativa.

### RevenueCat (RevenueCat, Inc., Stati Uniti): acquisti e abbonamento

Cosa riceve:
- Le informazioni sul tuo acquisto e abbonamento: prodotto, date, prezzo, valuta, store e
  stato della prova e del rinnovo.
- Un identificativo utente casuale creato da RevenueCat al primo avvio dell'app. Non è il
  tuo nome, la tua email né il tuo account Apple o Google.
- Dati tecnici di base: versione dell'app, sistema operativo e impostazioni di lingua e
  area geografica.
- Questi campi di misurazione:
  - paywall_trigger: cosa ha aperto la schermata PRO (una ricerca con la fotocamera,
    un'eliminazione multipla, uno spostamento multiplo in un album o il pulsante nelle
    Impostazioni).
  - batch_size: quante foto avevi selezionato quando la schermata PRO si è aperta da
    un'azione multipla.
  - gallery_size: la dimensione della galleria per fasce (meno di 3.000, da 3.000 a 10.000
    o oltre 10.000 foto). Inviato una sola volta, dopo la prima scansione.
  - use_case: solo se scegli di rispondere alla domanda facoltativa mostrata dopo un
    acquisto o dopo l'inizio di una prova gratuita: per cosa usi soprattutto iSIMILAR
    (riparazione e servizio tecnico; cantieri, installazioni o ispezioni; un portfolio; un
    altro tipo di lavoro; pulire meme e screenshot; prodotti, acquisti e foto quotidiane;
    oppure qualcos'altro). Puoi saltarla.

Perché: gestire, convalidare e ripristinare l'abbonamento, e capire quali funzioni portano
a scegliere PRO e per cosa viene usata l'app.

### Firebase Crashlytics (Google): report degli errori

Cosa riceve: report di arresti anomali ed errori (dettagli tecnici dell'errore e stato
dell'app in quel momento), modello del dispositivo, versione del sistema operativo e
versione dell'app, associati a un identificativo di installazione.

Perché: trovare e correggere gli errori.

### Firebase Remote Config (Google): aggiornamenti obbligatori

Cosa riceve: impostazioni di paese e lingua, fuso orario, versione del sistema operativo e
identificativi dell'app, associati a un identificativo di installazione Firebase.

Perché: sapere qual è la versione minima dell'app ancora funzionante e, se la tua è
precedente, chiederti di aggiornarla.

### Firebase Cloud Messaging (Google): notifiche

Cosa riceve: un token per le notifiche associato a un identificativo di installazione
Firebase, modello del dispositivo, lingua, fuso orario, versione del sistema operativo e
versione dell'app. Il token viene creato all'avvio dell'app; le notifiche vengono mostrate
solo se le consenti.

Perché: inviarti avvisi sull'app e sulle nuove versioni (vedi sezione 6).

### Cosa non riceve nessuno di questi fornitori

Le tue foto, le miniature, i vettori, la foto che scatti con la fotocamera o qualsiasi
altro contenuto della galleria.

### Pagamenti

I pagamenti sono gestiti da Apple (App Store) o Google (Google Play) secondo i loro termini
e le loro informative. Non vediamo mai i dati della tua carta o del tuo conto; riceviamo
solo lo stato dell'acquisto tramite RevenueCat.

## 6. Notifiche

iSIMILAR invia solo:
- un promemoria settimanale facoltativo per rivedere le foto nuove, che attivi nell'app.
  Viene creato sul telefono e non invia alcun dato;
- avvisi sull'app e sulle nuove versioni, tramite Firebase Cloud Messaging.

Non inviamo notifiche promozionali o pubblicitarie. Puoi disattivare le notifiche in
qualsiasi momento dalle impostazioni del telefono, e il promemoria settimanale dalle
Impostazioni dell'app.

## 7. Base giuridica (GDPR)

- Vendere, convalidare e ripristinare l'abbonamento: esecuzione di un contratto
  (art. 6, par. 1, lett. b GDPR).
- Report degli errori e verifica degli aggiornamenti obbligatori: nostro legittimo
  interesse a far funzionare l'app in modo sicuro (art. 6, par. 1, lett. f).
- I campi di misurazione paywall_trigger, batch_size e gallery_size: nostro legittimo
  interesse a capire quali funzioni portano a scegliere PRO, con un insieme ridotto di dati
  che non include mai le tue foto (art. 6, par. 1, lett. f). [ABOGADO]
- La tua risposta alla domanda facoltativa use_case: il tuo consenso, dato scegliendo di
  rispondere (art. 6, par. 1, lett. a). Puoi revocarlo in qualsiasi momento chiedendoci di
  cancellarla. [ABOGADO]
- Notifiche: il tuo consenso, dato tramite la richiesta di autorizzazione del telefono
  (art. 6, par. 1, lett. a); il token è necessario per inviarti gli avvisi che consenti
  (art. 6, par. 1, lett. f). [ABOGADO]
- Rispondere alle tue email e richieste: nostro legittimo interesse a risponderti e, per le
  richieste sulla privacy, un obbligo di legge (art. 6, par. 1, lett. f e c).

Quando la base è il legittimo interesse, hai il diritto di opporti (sezione 10).

## 8. Trasferimenti internazionali

RevenueCat e Google possono trattare dati negli Stati Uniti.
- RevenueCat, Inc.: clausole contrattuali tipo della Commissione europea, incluse nel suo
  accordo sul trattamento dei dati.
- Google LLC (Firebase): Google aderisce al Data Privacy Framework UE-USA; i termini di
  Firebase includono anche le clausole contrattuali tipo.

Questi fornitori si avvalgono a loro volta di sub-responsabili vincolati agli stessi
obblighi. Puoi chiederci una copia delle garanzie. [ABOGADO]

## 9. Per quanto tempo conserviamo i dati

- Dati sul telefono: finché non usi Impostazioni > Reimposta App o disinstalli l'app.
- Report degli errori (Crashlytics): 90 giorni; poi Google inizia a cancellarli dai suoi
  sistemi.
- Identificativi di installazione Firebase (Remote Config, Cloud Messaging): finché non
  vengono cancellati; dopo la cancellazione, Google li rimuove dai suoi sistemi entro 180
  giorni. [VERIFICAR]
- Dati di acquisto e campi di misurazione (RevenueCat): finché l'abbonamento è attivo e per
  [PLAZO: propuesta, 3 anni dall'ultima attività] dopo, oppure finché non ci chiedi di
  cancellarli. [DECIDIR] [ABOGADO]
- Email che ci invii: [PLAZO: propuesta, 24 mesi dall'ultimo messaggio]. [DECIDIR]

Apple e Google conservano i propri registri degli acquisti secondo le loro politiche.

## 10. I tuoi diritti

Puoi chiederci di accedere ai tuoi dati, rettificarli, cancellarli, limitarne il
trattamento, riceverne una copia e opporti al trattamento basato sul legittimo interesse
(artt. 15-21 GDPR). Se il trattamento si basa sul consenso, puoi revocarlo in qualsiasi
momento, senza effetti su quanto fatto prima.

Poiché non esistono account, ci serve il tuo ID iSIMILAR per trovare i tuoi dati in
RevenueCat (vedi sezione 11). I report degli errori e gli identificativi Firebase non sono
associati a quell'ID, quindi non possiamo sapere quali sono tuoi (art. 11 GDPR); restano
comunque validi i tempi della sezione 9.

Ti risponderemo entro un mese. Puoi anche proporre reclamo al Garante per la protezione dei
dati personali (www.garanteprivacy.it) o all'autorità del paese UE in cui vivi o lavori.

## 11. Cancellare i tuoi dati

Puoi cancellare in qualsiasi momento i dati sul telefono e chiederci di cancellare quelli
conservati dai nostri fornitori. Istruzioni passo per passo: [URL DE LA PÁGINA DE BORRADO]

Cancellare i dati non annulla l'abbonamento. Per annullarlo, vedi i Termini d'uso.

## 12. Età

Devi avere almeno 14 anni, o l'età minima prevista dalla legge del tuo paese se superiore,
per utilizzare iSIMILAR.

Non raccogliamo consapevolmente dati di persone al di sotto di questa età. Se pensi che sia
successo, scrivici e li cancelleremo.

## 13. Decisioni automatizzate

Non prendiamo decisioni che ti riguardano basate unicamente su un trattamento
automatizzato e non creiamo profili pubblicitari.

## 14. Modifiche a questa informativa

Se cambia il modo in cui l'app usa i dati, aggiorneremo questa pagina e la data in alto
prima che la modifica arrivi nell'app. Se la modifica è importante, te lo diremo anche
nell'app.

## 15. Contatti

[EMAIL DE CONTACTO]
```

### 1.4 [SI SE ACTIVA ANALYTICS] Bloque para añadir cuando se resuelva el consentimiento

**No forma parte del texto principal.** Se publica el mismo día que la versión de la app con Firebase
Analytics, y solo si antes se ha decidido la base jurídica **[ABOGADO]**. Si el abogado concluye que hace
falta consentimiento, la app necesita antes una pantalla de aceptación y `analytics_service.dart:63`
(`analyticsStorageConsentGranted: true`) debe depender de la respuesta del usuario.

Se inserta en el apartado 5 de la política, después de Cloud Messaging; y se añaden las líneas indicadas
en los apartados 7 y 9. El valor `remove_album` solo se nombra si Anibal confirma que se registra así
(pendiente en `definicion-tecnica.md` · "Pendiente de confirmar").

**EN**
```
### Google Analytics for Firebase (Google): how the app is used

What it receives: usage events, namely scan started and completed (number of photos and
duration), search from the gallery or with the camera, actions on photos (delete, move to
an album, [remove from an album,] share; number of photos; whether it was a batch action;
whether the PRO screen was shown), PRO screen shown and what opened it, and your answer
to the optional use_case question, together with basic device and app data (model,
operating system, app version, language and country), linked to an app-instance
identifier. It never receives your photos, thumbnails, vectors or any image content.
Collection of the advertising identifier is disabled and advertising signals are set to
"denied".

Why: to understand how the app is used and improve it.

[Section 7] Usage analytics: [ABOGADO: consent (Art. 6(1)(a)), given in the app and
withdrawable in Settings, or legitimate interest (Art. 6(1)(f))].
[Section 9] Usage events (Firebase Analytics): [COMPLETAR: periodo configurado en la
consola, 2 o 14 meses].
```

**ES**
```
### Google Analytics para Firebase (Google): cómo se usa la app

Qué recibe: eventos de uso, es decir, escaneo iniciado y completado (número de fotos y
duración), búsqueda desde la galería o con la cámara, acciones sobre fotos (borrar, mover
a un álbum, [quitar de un álbum,] compartir; número de fotos; si fue una acción en lote;
si se mostró la pantalla de PRO), pantalla de PRO mostrada y qué la abrió, y tu respuesta
a la pregunta opcional use_case, junto con datos básicos del dispositivo y de la app
(modelo, sistema operativo, versión de la app, idioma y país), asociados a un
identificador de instancia de la app. Nunca recibe tus fotos, miniaturas, vectores ni
ningún contenido de las imágenes. La recogida del identificador publicitario está
desactivada y las señales de publicidad, denegadas.

Para qué: entender cómo se usa la app y mejorarla.

[Apartado 7] Analítica de uso: [ABOGADO: consentimiento (art. 6.1.a), dado en la app y
revocable en Ajustes, o interés legítimo (art. 6.1.f)].
[Apartado 9] Eventos de uso (Firebase Analytics): [COMPLETAR: 2 o 14 meses].
```

**IT**
```
### Google Analytics per Firebase (Google): come viene usata l'app

Cosa riceve: eventi di utilizzo, cioè scansione avviata e completata (numero di foto e
durata), ricerca dalla galleria o con la fotocamera, azioni sulle foto (eliminare,
spostare in un album, [togliere da un album,] condividere; numero di foto; se si tratta di
un'azione multipla; se è stata mostrata la schermata PRO), schermata PRO mostrata e cosa
l'ha aperta, e la tua risposta alla domanda facoltativa use_case, insieme a dati di base
del dispositivo e dell'app (modello, sistema operativo, versione dell'app, lingua e
paese), associati a un identificativo dell'istanza dell'app. Non riceve mai le tue foto,
miniature, vettori o qualsiasi contenuto delle immagini. La raccolta dell'identificativo
pubblicitario è disattivata e i segnali pubblicitari sono negati.

Perché: capire come viene usata l'app e migliorarla.

[Sezione 7] Analisi dell'utilizzo: [ABOGADO: consenso (art. 6, par. 1, lett. a), dato
nell'app e revocabile nelle Impostazioni, o legittimo interesse (art. 6, par. 1, lett. f)].
[Sezione 9] Eventi di utilizzo (Firebase Analytics): [COMPLETAR: 2 o 14 mesi].
```

**Cambios el mismo día en las tiendas** (además de la fecha de la política):
- App Store: el `ID de dispositivo` gana la finalidad "Analytics"; la `Interacción con el producto` ya
  existe. Revisar con la guía de Google Analytics que enlaza Firebase (support.google.com/analytics/answer/11582702)
  si hay que declarar algo más. [VERIFICAR]
- Google Play: `Interacciones con la app` y `ID de dispositivo u otros` reciben la fuente Firebase
  Analytics, finalidad "Análisis".

---

## 2. Términos de uso

### 2.1 Terms of Use (EN)

```
# iSIMILAR Terms of Use

Last updated: [FECHA DE PUBLICACIÓN]

## 1. Who we are and what these terms cover

iSIMILAR is provided by [NOMBRE COMPLETO], [DIRECCIÓN], VAT number (P. IVA) [P. IVA],
email [EMAIL DE CONTACTO] ("we", "us").

These terms apply to the iSIMILAR app for iOS and Android. By using the app you accept
them. If you downloaded iSIMILAR from the App Store, Apple's Standard Licensed
Application End User License Agreement
(https://www.apple.com/legal/internet-services/itunes/dev/stdeula/) also applies.
[ABOGADO: relación entre estos términos y el EULA estándar de Apple]

How we handle data is explained in the Privacy Policy: [URL DE LA POLÍTICA]

## 2. Age

You must be at least 14 years old, or the minimum age required by the laws of your
country if higher, to use iSIMILAR.

[ABOGADO: añadir, si procede, que las compras de menores de 18 años requieren la
autorización de sus padres o tutores, según las reglas de Apple y Google.]

## 3. What iSIMILAR does, and what it does not

iSIMILAR finds photos in your gallery that look like a photo you choose or take with the
camera. It compares shape, texture, colour and composition. It works on your phone,
without an internet connection, and your photos never leave the device.

Results are based on visual similarity, not on exact identification. The app may show
photos that are not related and may miss photos that are. It does not search by text,
date, location or person, it does not recognise faces and it does not name objects. Do
not rely on it where you need certainty, such as evidence or medical decisions.

## 4. Free and PRO

Free:
- Gallery scan.
- Unlimited searches from photos saved on your phone.
- 5 searches with the camera.
- Deleting photos one at a time.

iSIMILAR PRO:
- Unlimited searches with the camera.
- Batch actions: deleting or moving many photos at once.

## 5. Subscription, free trial and renewal

- iSIMILAR PRO is an annual subscription that renews automatically.
- Price: 12 € per year in the euro area and 11.99 USD per year in the United States; in
  other countries, the equivalent price set by the App Store or Google Play. The exact
  price, in your currency and with any taxes that apply, is shown in the app and in the
  store's confirmation screen before you pay.
- Free trial: new subscribers who are eligible under the store's rules get 7 days free.
  The trial starts when you confirm the subscription. If you do not cancel, the annual
  price is charged when the trial ends.
- Renewal: the subscription renews every year at the price in force at that time unless
  you cancel before the current period ends. If the price changes, the store will tell
  you in advance and, where required, ask for your consent.
- To avoid being charged, cancel at least 24 hours before the end of the free trial or of
  the current period. [VERIFICAR: Google Play no publica este plazo]
- Payment is charged to your Apple ID or Google account by Apple or Google. We never see
  or store your payment details.

How to cancel:
- iPhone or iPad: Settings > [your name] > Subscriptions > iSIMILAR > Cancel
  Subscription, or https://apps.apple.com/account/subscriptions
- Android: Google Play > your profile icon > Payments & subscriptions > Subscriptions >
  iSIMILAR > Cancel subscription, or
  https://play.google.com/store/account/subscriptions

Uninstalling the app does not cancel the subscription. After you cancel, you keep PRO
until the end of the period you have already paid for.

Restore Purchases: if you change phones or reinstall the app, tap "Restore Purchases" in
the app, signed in with the same Apple ID or Google account.

## 6. Refunds

Purchases are processed by Apple or Google, and refund requests are handled by them under
their own terms. This does not affect your rights as a consumer under the law. [ABOGADO]

## 7. Your photos and your decisions

You decide what to delete, move or share. The app always shows a preview and asks for
confirmation. Check the results before you confirm: a deleted photo may not be
recoverable from iSIMILAR, although your phone may keep it for a while in its recently
deleted folder. Keep a backup of the photos that matter to you.

## 8. Licence and acceptable use

We give you a personal, non-exclusive, non-transferable licence to use iSIMILAR on devices
you own or control. You may not copy, modify, decompile, reverse engineer, resell or
redistribute the app, or try to get around its payment system, except where the law
allows it.

## 9. Intellectual property

The app, its design, code and visual model belong to us or to our licensors. These terms
do not give you any ownership rights. Your photos are yours; we have no access to them.

## 10. Updates and required updates

We may update the app to fix errors, improve it or keep it secure. If a version stops
being supported, the app may ask you to update before you can continue using it.

## 11. Liability

[ABOGADO: revisar el texto siguiente contra el Codice del Consumo y el Codice civile.]

We provide the app with reasonable care. Nothing in these terms limits or excludes our
liability where the law does not allow it, including liability for intent or gross
negligence, or your legal rights as a consumer, including your rights if the app does not
conform to what was agreed. Within those limits, we are not liable for losses that were
not reasonably foreseeable, or for photos you delete, move or share after confirming the
action.

## 12. Changes to these terms

We may update these terms. The date above shows the current version. If a change is
significant, we will tell you in the app before it applies. If you do not accept it, you
can cancel your subscription and stop using the app.

## 13. Applicable law and disputes

These terms are governed by Italian law. If you are a consumer, you keep the protection
of the mandatory laws of the country where you live, and you can go to the courts of that
country. [ABOGADO]

## 14. Contact

[EMAIL DE CONTACTO]
```

### 2.2 Términos de uso (ES)

```
# Términos de uso de iSIMILAR

Última actualización: [FECHA DE PUBLICACIÓN]

## 1. Quiénes somos y qué cubren estos términos

iSIMILAR la ofrece [NOMBRE COMPLETO], [DIRECCIÓN], P. IVA [P. IVA], correo
[EMAIL DE CONTACTO] ("nosotros").

Estos términos se aplican a la app iSIMILAR para iOS y Android. Al usar la app los
aceptas. Si descargaste iSIMILAR desde la App Store, también se aplica el Contrato de
licencia de usuario final estándar de Apple
(https://www.apple.com/legal/internet-services/itunes/dev/stdeula/).
[ABOGADO: relación entre estos términos y el EULA estándar de Apple]

Cómo tratamos los datos se explica en la Política de privacidad: [URL DE LA POLÍTICA]

## 2. Edad

Debes tener al menos 14 años, o la edad mínima que exija la ley de tu país si es mayor,
para usar iSIMILAR.

[ABOGADO: añadir, si procede, que las compras de menores de 18 años requieren la
autorización de sus padres o tutores, según las reglas de Apple y Google.]

## 3. Qué hace iSIMILAR y qué no

iSIMILAR encuentra en tu galería las fotos que se parecen a una que eliges o que haces con
la cámara. Compara forma, textura, color y composición. Funciona en tu teléfono, sin
conexión a internet, y tus fotos nunca salen del dispositivo.

Los resultados se basan en el parecido visual, no en una identificación exacta. La app
puede mostrar fotos que no tienen relación y dejar fuera otras que sí la tienen. No busca
por texto, fecha, ubicación ni persona, no reconoce caras y no nombra objetos. No la uses
como única fuente cuando necesites certeza, por ejemplo como prueba o para decisiones
médicas.

## 4. Gratis y PRO

Gratis:
- Escaneo de la galería.
- Búsquedas ilimitadas desde fotos guardadas en el teléfono.
- 5 búsquedas con la cámara.
- Borrado de fotos de una en una.

iSIMILAR PRO:
- Búsquedas con la cámara ilimitadas.
- Acciones en lote: borrar o mover muchas fotos de una vez.

## 5. Suscripción, prueba gratuita y renovación

- iSIMILAR PRO es una suscripción anual que se renueva automáticamente.
- Precio: 12 € al año en la zona euro y 11,99 USD al año en Estados Unidos; en otros
  países, el equivalente que fija la App Store o Google Play. El precio exacto, en tu
  moneda y con los impuestos aplicables, se muestra en la app y en la pantalla de
  confirmación de la tienda antes de pagar.
- Prueba gratuita: los nuevos suscriptores que cumplan los requisitos de la tienda tienen
  7 días gratis. La prueba empieza al confirmar la suscripción. Si no cancelas, el precio
  anual se cobra al terminar la prueba.
- Renovación: la suscripción se renueva cada año al precio vigente en ese momento salvo
  que la canceles antes de que termine el periodo en curso. Si el precio cambia, la tienda
  te avisará antes y, cuando sea obligatorio, te pedirá tu conformidad.
- Para que no se te cobre, cancela al menos 24 horas antes del final de la prueba gratuita
  o del periodo en curso. [VERIFICAR: Google Play no publica este plazo]
- El cobro lo hace Apple o Google en tu Apple ID o tu cuenta de Google. Nunca vemos ni
  guardamos tus datos de pago.

Cómo cancelar:
- iPhone o iPad: Ajustes > [tu nombre] > Suscripciones > iSIMILAR > Cancelar suscripción,
  o https://apps.apple.com/account/subscriptions
- Android: Google Play > icono de tu perfil > Pagos y suscripciones > Suscripciones >
  iSIMILAR > Cancelar suscripción, o https://play.google.com/store/account/subscriptions

Desinstalar la app no cancela la suscripción. Después de cancelar, mantienes PRO hasta el
final del periodo que ya has pagado.

Restaurar compras: si cambias de teléfono o reinstalas la app, toca "Restaurar compras" en
la app con el mismo Apple ID o la misma cuenta de Google.

## 6. Reembolsos

Las compras las procesa Apple o Google, y las solicitudes de reembolso las gestionan ellos
según sus propios términos. Esto no afecta a tus derechos como consumidor según la ley.
[ABOGADO]

## 7. Tus fotos y tus decisiones

Tú decides qué borrar, mover o compartir. La app siempre muestra una vista previa y pide
confirmación. Revisa los resultados antes de confirmar: una foto borrada puede no ser
recuperable desde iSIMILAR, aunque tu teléfono puede conservarla un tiempo en su carpeta
de eliminados recientemente. Ten copia de las fotos que te importan.

## 8. Licencia y uso aceptable

Te concedemos una licencia personal, no exclusiva e intransferible para usar iSIMILAR en
dispositivos que sean tuyos o que controles. No puedes copiar, modificar, descompilar,
aplicar ingeniería inversa, revender ni redistribuir la app, ni intentar saltarte su
sistema de pago, salvo donde la ley lo permita.

## 9. Propiedad intelectual

La app, su diseño, su código y su modelo visual son nuestros o de quienes nos los
licencian. Estos términos no te dan ningún derecho de propiedad. Tus fotos son tuyas; no
tenemos acceso a ellas.

## 10. Actualizaciones y actualizaciones obligatorias

Podemos actualizar la app para corregir errores, mejorarla o mantenerla segura. Si una
versión deja de tener soporte, la app puede pedirte que actualices antes de seguir
usándola.

## 11. Responsabilidad

[ABOGADO: revisar el texto siguiente contra el Codice del Consumo y el Codice civile.]

Ofrecemos la app con una diligencia razonable. Nada de estos términos limita ni excluye
nuestra responsabilidad cuando la ley no lo permite, incluida la responsabilidad por dolo
o culpa grave, ni tus derechos legales como consumidor, incluidos tus derechos si la app
no es conforme con lo acordado. Dentro de esos límites, no respondemos de daños que no
fueran razonablemente previsibles ni de las fotos que borres, muevas o compartas después
de confirmar la acción.

## 12. Cambios en estos términos

Podemos actualizar estos términos. La fecha de arriba indica la versión vigente. Si un
cambio es importante, te lo diremos en la app antes de que se aplique. Si no lo aceptas,
puedes cancelar la suscripción y dejar de usar la app.

## 13. Ley aplicable y conflictos

Estos términos se rigen por la ley italiana. Si eres consumidor, conservas la protección
de las normas imperativas del país en el que vives y puedes acudir a los tribunales de ese
país. [ABOGADO]

## 14. Contacto

[EMAIL DE CONTACTO]
```

### 2.3 Termini d'uso (IT)

```
# Termini d'uso di iSIMILAR

Ultimo aggiornamento: [FECHA DE PUBLICACIÓN]

## 1. Chi siamo e cosa coprono questi termini

iSIMILAR è fornita da [NOMBRE COMPLETO], [DIRECCIÓN], P. IVA [P. IVA], email
[EMAIL DE CONTACTO] ("noi").

Questi termini si applicano all'app iSIMILAR per iOS e Android. Usando l'app li accetti.
Se hai scaricato iSIMILAR dall'App Store, si applica anche il Contratto di licenza
standard per l'utente finale di Apple
(https://www.apple.com/legal/internet-services/itunes/dev/stdeula/).
[ABOGADO: relación entre estos términos y el EULA estándar de Apple]

Il trattamento dei dati è spiegato nell'Informativa sulla privacy: [URL DE LA POLÍTICA]

## 2. Età

Devi avere almeno 14 anni, o l'età minima prevista dalla legge del tuo paese se superiore,
per utilizzare iSIMILAR.

[ABOGADO: añadir, si procede, que las compras de menores de 18 años requieren la
autorización de sus padres o tutores, según las reglas de Apple y Google.]

## 3. Cosa fa iSIMILAR e cosa non fa

iSIMILAR trova nella tua galleria le foto che somigliano a una foto che scegli o che
scatti con la fotocamera. Confronta forma, texture, colore e composizione. Funziona sul
telefono, senza connessione a internet, e le tue foto non escono mai dal dispositivo.

I risultati si basano sulla somiglianza visiva, non su un'identificazione esatta. L'app
può mostrare foto non correlate e non trovarne altre che lo sono. Non cerca per testo,
data, luogo o persona, non riconosce i volti e non dà un nome agli oggetti. Non usarla
come unica fonte quando ti serve certezza, per esempio come prova o per decisioni
mediche.

## 4. Gratis e PRO

Gratis:
- Scansione della galleria.
- Ricerche illimitate da foto salvate sul telefono.
- 5 ricerche con la fotocamera.
- Eliminazione delle foto una alla volta.

iSIMILAR PRO:
- Ricerche con la fotocamera illimitate.
- Azioni multiple: eliminare o spostare molte foto in una volta.

## 5. Abbonamento, prova gratuita e rinnovo

- iSIMILAR PRO è un abbonamento annuale a rinnovo automatico.
- Prezzo: 12 € all'anno nell'area euro e 11,99 USD all'anno negli Stati Uniti; negli
  altri paesi, l'equivalente stabilito dall'App Store o da Google Play. Il prezzo esatto,
  nella tua valuta e con le eventuali imposte, è mostrato nell'app e nella schermata di
  conferma dello store prima del pagamento.
- Prova gratuita: i nuovi abbonati idonei secondo le regole dello store hanno 7 giorni
  gratis. La prova inizia quando confermi l'abbonamento. Se non annulli, il prezzo annuale
  viene addebitato alla fine della prova.
- Rinnovo: l'abbonamento si rinnova ogni anno al prezzo in vigore in quel momento, salvo
  annullamento prima della fine del periodo in corso. Se il prezzo cambia, lo store ti
  avviserà prima e, quando richiesto, ti chiederà il consenso.
- Per evitare l'addebito, annulla almeno 24 ore prima della fine della prova gratuita o del
  periodo in corso. [VERIFICAR: Google Play no publica este plazo]
- L'addebito è effettuato da Apple o Google sul tuo ID Apple o account Google. Non vediamo
  né conserviamo mai i tuoi dati di pagamento.

Come annullare:
- iPhone o iPad: Impostazioni > [il tuo nome] > Abbonamenti > iSIMILAR > Annulla
  abbonamento, oppure https://apps.apple.com/account/subscriptions
- Android: Google Play > icona del profilo > Pagamenti e abbonamenti > Abbonamenti >
  iSIMILAR > Annulla abbonamento, oppure https://play.google.com/store/account/subscriptions

Disinstallare l'app non annulla l'abbonamento. Dopo l'annullamento, mantieni PRO fino alla
fine del periodo già pagato.

Ripristina acquisti: se cambi telefono o reinstalli l'app, tocca "Ripristina acquisti"
nell'app con lo stesso ID Apple o account Google.

## 6. Rimborsi

Gli acquisti sono gestiti da Apple o Google, e le richieste di rimborso sono trattate da
loro secondo i rispettivi termini. Questo non pregiudica i tuoi diritti di consumatore
previsti dalla legge. [ABOGADO]

## 7. Le tue foto e le tue decisioni

Sei tu a decidere cosa eliminare, spostare o condividere. L'app mostra sempre
un'anteprima e chiede conferma. Controlla i risultati prima di confermare: una foto
eliminata potrebbe non essere recuperabile da iSIMILAR, anche se il telefono potrebbe
conservarla per un po' nella cartella degli elementi eliminati di recente. Tieni un backup
delle foto importanti.

## 8. Licenza e uso consentito

Ti concediamo una licenza personale, non esclusiva e non trasferibile per usare iSIMILAR
su dispositivi di tua proprietà o sotto il tuo controllo. Non puoi copiare, modificare,
decompilare, decodificare, rivendere o ridistribuire l'app, né tentare di aggirarne il
sistema di pagamento, salvo nei casi consentiti dalla legge.

## 9. Proprietà intellettuale

L'app, il suo design, il codice e il modello visivo appartengono a noi o ai nostri
licenzianti. Questi termini non ti attribuiscono alcun diritto di proprietà. Le tue foto
sono tue; non abbiamo accesso ad esse.

## 10. Aggiornamenti e aggiornamenti obbligatori

Possiamo aggiornare l'app per correggere errori, migliorarla o mantenerla sicura. Se una
versione non è più supportata, l'app può chiederti di aggiornarla prima di continuare a
usarla.

## 11. Responsabilità

[ABOGADO: revisar el texto siguiente contra el Codice del Consumo y el Codice civile.]

Forniamo l'app con ragionevole diligenza. Nulla in questi termini limita o esclude la
nostra responsabilità quando la legge non lo consente, compresa la responsabilità per dolo
o colpa grave, né i tuoi diritti di consumatore, compresi i diritti in caso di difetto di
conformità dell'app. Entro questi limiti, non rispondiamo di danni non ragionevolmente
prevedibili né delle foto che elimini, sposti o condividi dopo aver confermato l'azione.

## 12. Modifiche ai termini

Possiamo aggiornare questi termini. La data in alto indica la versione in vigore. Se una
modifica è importante, te lo diremo nell'app prima che si applichi. Se non la accetti,
puoi annullare l'abbonamento e smettere di usare l'app.

## 13. Legge applicabile e controversie

Questi termini sono regolati dalla legge italiana. Se sei un consumatore, mantieni la
protezione delle norme imperative del paese in cui vivi e puoi rivolgerti ai giudici di
quel paese. [ABOGADO]

## 14. Contatti

[EMAIL DE CONTACTO]
```

**Notas de los términos**
- Plazo de 24 horas, verificado el 22-10-2026:
  - Apple, prueba gratuita: verificado. support.apple.com/en-us/118428: *"If you signed up for a trial
    subscription and you don't want to renew it, cancel it at least 24 hours before the trial ends."*
  - Apple, renovación: la página de soporte no da plazo. La documentación de StoreKit ("Handling
    Subscriptions Billing") dice: *"During the 24-hour period before the subscription expires, the App
    Store starts trying to renew it automatically."* El plazo de 24 h se deduce de eso; es coherente,
    pero no es una cita literal.
  - Google Play: **no he encontrado plazo** en support.google.com/googleplay/answer/7018481 ni en la
    política de suscripciones (answer/9900533). Por eso el texto lo presenta como consejo ("para que no
    se te cobre, cancela al menos 24 h antes"), que es prudente en ambas tiendas y no atribuye la regla
    a Google. Si prefieres no arriesgar, quita el [VERIFICAR] y deja la frase tal cual; o bien sepárala
    por tienda.
- Ruta de cancelación en Android: Google solo dice "Open your subscriptions page in Google Play". Los
  nombres exactos de los menús ("Pagos y suscripciones") [VERIFICAR] en un teléfono en cada idioma.
- He eliminado de los términos antiguos: créditos, "5 free camera searches" como "Trial", la ley
  española, la indemnización ilimitada a cargo del usuario y el tope de responsabilidad de 12 meses
  (probablemente nulo frente a consumidores; [ABOGADO]).
- Tampoco incluyo el enlace a la plataforma europea de resolución de litigios en línea (ODR): según
  tengo entendido se cerró en julio de 2025. [VERIFICAR] antes de que alguien lo añada por costumbre.

---

## 3. Página de borrado de datos

URL propuesta: `isimilar.app/delete-data` (y `/es/…`, `/it/…`). Sustituye a la página de Notion
`Data-Deletion-iSimilar-32388278a02e80f3a0f6c6cf12028e33`, que abre el botón "Eliminar mis datos" de
Ajustes (`settings_view.dart:664`).

### 3.1 Delete your data (EN)

```
# Delete your iSIMILAR data

iSIMILAR has no accounts. Your photos and the search index never leave your phone. A
small amount of technical data about purchases, usage and errors is held by our service
providers, linked to random identifiers. This page explains how to delete both.

## 1. Data on your phone

- Reset the app: open iSIMILAR > Settings > Reset App. This deletes the visual index and
  the analysis data, and undoes the albums created in the app. Your photos are not
  deleted.
- Delete everything: uninstall iSIMILAR. This deletes all the data the app stores on your
  phone. Your photos are not deleted.

## 2. Data held by our providers

1. Copy your iSIMILAR ID: open iSIMILAR > Settings, then press and hold the version number
   at the bottom of the screen. You will see "ID copied".
2. Email [EMAIL DE CONTACTO] with the subject "Delete my data" and paste your ID.
3. We will delete the record linked to that ID in RevenueCat: your purchase and
   subscription information and the measurement fields (paywall_trigger, batch_size,
   gallery_size and, if you answered it, use_case). We will confirm by email within one
   month.

If you can no longer open the app, send us the store and the approximate date of your
purchase, and the order number from your Apple or Google receipt if you have it. We will
try to find your record with that information.

## 3. What we cannot delete, and why

- Error reports (Firebase Crashlytics) and Firebase installation identifiers are not
  linked to your iSIMILAR ID, so we cannot find which ones are yours. Error reports are
  deleted automatically after 90 days. Once you uninstall the app, it stops sending any
  data.
- Apple and Google keep their own records of your purchases. To manage them, contact
  Apple or Google.

## 4. Your subscription

Deleting your data does not cancel your subscription:
- iPhone or iPad: Settings > [your name] > Subscriptions, or
  https://apps.apple.com/account/subscriptions
- Android: Google Play > Payments & subscriptions > Subscriptions, or
  https://play.google.com/store/account/subscriptions

If you use "Restore Purchases" after we delete your data, a new record is created so
that you keep PRO.

## 5. Questions

[EMAIL DE CONTACTO] · More details in the Privacy Policy: [URL DE LA POLÍTICA]
```

### 3.2 Borrar tus datos (ES)

```
# Borrar tus datos de iSIMILAR

iSIMILAR no tiene cuentas. Tus fotos y el índice de búsqueda nunca salen de tu teléfono.
Nuestros proveedores guardan una pequeña cantidad de datos técnicos de compras, uso y
errores, asociados a identificadores aleatorios. Esta página explica cómo borrar ambos.

## 1. Datos en tu teléfono

- Restablecer la app: abre iSIMILAR > Ajustes > Restablecer App. Se borran el índice
  visual y los datos de análisis, y se deshacen los álbumes creados en la app. Tus fotos
  no se borran.
- Borrarlo todo: desinstala iSIMILAR. Se borran todos los datos que la app guarda en tu
  teléfono. Tus fotos no se borran.

## 2. Datos que guardan nuestros proveedores

1. Copia tu ID de iSIMILAR: abre iSIMILAR > Ajustes y mantén pulsado el número de versión,
   al final de la pantalla. Verás el aviso "ID copied".
2. Escribe a [EMAIL DE CONTACTO] con el asunto "Borrar mis datos" y pega tu ID.
3. Borraremos el registro asociado a ese ID en RevenueCat: la información de tu compra y
   tu suscripción y los campos de medición (paywall_trigger, batch_size, gallery_size y,
   si respondiste, use_case). Te lo confirmaremos por correo en el plazo de un mes.

Si ya no puedes abrir la app, envíanos la tienda y la fecha aproximada de la compra, y el
número de pedido del recibo de Apple o Google si lo tienes. Intentaremos encontrar tu
registro con esos datos.

## 3. Lo que no podemos borrar, y por qué

- Los informes de errores (Firebase Crashlytics) y los identificadores de instalación de
  Firebase no están asociados a tu ID de iSIMILAR, así que no podemos saber cuáles son
  tuyos. Los informes de errores se borran solos a los 90 días. Al desinstalar la app,
  deja de enviar cualquier dato.
- Apple y Google conservan sus propios registros de tus compras. Para gestionarlos,
  contacta con Apple o Google.

## 4. Tu suscripción

Borrar tus datos no cancela la suscripción:
- iPhone o iPad: Ajustes > [tu nombre] > Suscripciones, o
  https://apps.apple.com/account/subscriptions
- Android: Google Play > Pagos y suscripciones > Suscripciones, o
  https://play.google.com/store/account/subscriptions

Si usas "Restaurar compras" después de que borremos tus datos, se crea un registro nuevo
para que mantengas PRO.

## 5. Dudas

[EMAIL DE CONTACTO] · Más detalles en la Política de privacidad: [URL DE LA POLÍTICA]
```

### 3.3 Cancellare i tuoi dati (IT)

```
# Cancellare i tuoi dati di iSIMILAR

iSIMILAR non ha account. Le tue foto e l'indice di ricerca non escono mai dal telefono. I
nostri fornitori conservano una piccola quantità di dati tecnici su acquisti, utilizzo ed
errori, associati a identificativi casuali. Questa pagina spiega come cancellare entrambi.

## 1. Dati sul telefono

- Reimpostare l'app: apri iSIMILAR > Impostazioni > Reimposta App. Vengono cancellati
  l'indice visivo e i dati di analisi, e vengono annullati gli album creati nell'app. Le
  tue foto non vengono eliminate.
- Cancellare tutto: disinstalla iSIMILAR. Vengono cancellati tutti i dati che l'app salva
  sul telefono. Le tue foto non vengono eliminate.

## 2. Dati conservati dai nostri fornitori

1. Copia il tuo ID iSIMILAR: apri iSIMILAR > Impostazioni e tieni premuto il numero di
   versione in fondo alla schermata. Vedrai il messaggio "ID copied".
2. Scrivi a [EMAIL DE CONTACTO] con oggetto "Cancella i miei dati" e incolla il tuo ID.
3. Cancelleremo il record associato a quell'ID in RevenueCat: le informazioni
   sull'acquisto e sull'abbonamento e i campi di misurazione (paywall_trigger, batch_size,
   gallery_size e, se hai risposto, use_case). Te lo confermeremo via email entro un mese.

Se non riesci più ad aprire l'app, inviaci lo store e la data approssimativa
dell'acquisto, e il numero d'ordine della ricevuta di Apple o Google se ce l'hai. Cercheremo
il tuo record con questi dati.

## 3. Cosa non possiamo cancellare, e perché

- I report degli errori (Firebase Crashlytics) e gli identificativi di installazione
  Firebase non sono associati al tuo ID iSIMILAR, quindi non possiamo sapere quali sono
  tuoi. I report degli errori vengono cancellati automaticamente dopo 90 giorni. Una volta
  disinstallata, l'app smette di inviare qualsiasi dato.
- Apple e Google conservano i propri registri degli acquisti. Per gestirli, contatta Apple
  o Google.

## 4. Il tuo abbonamento

Cancellare i dati non annulla l'abbonamento:
- iPhone o iPad: Impostazioni > [il tuo nome] > Abbonamenti, oppure
  https://apps.apple.com/account/subscriptions
- Android: Google Play > Pagamenti e abbonamenti > Abbonamenti, oppure
  https://play.google.com/store/account/subscriptions

Se usi "Ripristina acquisti" dopo che abbiamo cancellato i tuoi dati, viene creato un nuovo
record per mantenere PRO.

## 5. Domande

[EMAIL DE CONTACTO] · Maggiori dettagli nell'Informativa sulla privacy: [URL DE LA POLÍTICA]
```

**Notas de la página de borrado**
- Menús verificados en el código: "Reset App / Restablecer App / Reimposta App" (`intl_*.arb`, clave
  `reset_ratings`), con el mensaje de confirmación "All AI analysis data and albums created in the app
  will be deleted. Your device photos will not be deleted." (`reset_ai_confirm_message`). El aviso
  "ID copied" está fijo en inglés (`settings_view.dart:279`); por eso los textos ES e IT lo citan en
  inglés.
- Búsqueda de un cliente en RevenueCat por número de pedido: [VERIFICAR] en el panel. Si no se puede,
  quitar el párrafo "Si ya no puedes abrir la app…".
- Propuesta para la app, no solicitada (se reporta, no se ejecuta): un botón que copie el ID sin el
  gesto oculto de pulsación larga y, mejor aún, que borre en el propio teléfono los identificadores de
  Firebase (`FirebaseInstallations.delete()`). Eso haría el borrado más completo y fácil de encontrar,
  como recomienda Google.

---

## 4. Etiqueta de App Store y formulario de Google Play recomendados

### 4.0 Respuesta al pendiente de `definicion-tecnica.md` línea 78: ¿"vinculados" o no?

**Recomendación: declarar todos los tipos de datos como "vinculados a ti" ("Data Linked to You"), sin
rastreo.** Motivos, de más a menos fuerte:

1. **La definición de Apple es explícita.** App Privacy Details: *"'Personal Information' and 'Personal
   Data', as defined under relevant privacy laws, are considered linked to the user."* El responsable
   está en la UE, así que se aplica el RGPD, y para el RGPD los datos asociados a un ID de usuario o de
   instalación son datos personales (considerando 26). Nuestra propia política lo dice.
2. **No se cumplen las condiciones de Apple para "no vinculados".** Apple exige quitar *"any direct
   identifiers, such as user ID"* antes de recoger el dato y, después, *"You must not attempt to link
   the data back to the user's identity"*. RevenueCat recibe las compras con un ID de usuario, y el
   procedimiento de borrado consiste precisamente en que el usuario nos mande ese ID desde su correo.
3. **RevenueCat no lo contradice si se lee entero.** Su guía (revenuecat.com/docs/…/apple-app-privacy)
   permite responder "No" solo *"If you are using RevenueCat's anonymous app user ID's, and do not have
   a way to identify individual users"*. Tenemos esa forma: el ID copiado más el correo. La respuesta
   "No" de su blog parte de "IDs anónimos" y de no recoger datos personales, algo que el RGPD no
   reconoce en nuestro caso.
4. **Firebase no da criterio.** Su guía para la App Store (firebase.google.com/docs/ios/app-store-data-collection)
   dice *"It is your responsibility to ensure your privacy nutrition labels are accurate"* y no indica
   si los datos van vinculados. Crashlytics y Remote Config van asociados a un identificador de
   instalación: aplico el mismo criterio que en el punto 1.

**Qué cambia de verdad:** la ficha mostrará "Data Linked to You" en lugar de "Data Not Linked to You".
**No** implica rastreo, no aparece "Data Used to Track You", no obliga a pedir permiso con App Tracking
Transparency y no requiere enviar una versión nueva (Apple: *"you do not need to submit an app update in
order to change your answers"*). Coste: la etiqueta parece algo menos "limpia"; por eso la web debe
explicar en una frase qué es cada dato.

**Alternativa (no recomendada):** mantener "no vinculados" y dejar escrito el razonamiento de RevenueCat.
El riesgo es una etiqueta inexacta según la definición de Apple y contradicha por nuestra propia
política, que habla de datos personales seudónimos.

### 4.1 Etiqueta App Store recomendada (App Store Connect > App Privacy)

"¿Recogéis datos de esta app?": **Sí**. "¿Se usan para rastrear?": **No** en todos los tipos.

| Categoría > tipo de dato (nombre en App Store Connect) | Qué es en iSIMILAR | SDK | Vinculado | Rastreo | Finalidades |
|---|---|---|---|---|---|
| Purchases > Purchase History | Compras, suscripción, prueba y renovaciones | RevenueCat | **Sí** | No | App Functionality, Analytics (mínimo que exige RevenueCat) |
| Identifiers > User ID | ID de usuario aleatorio de RevenueCat (`$RCAnonymousID`) | RevenueCat | **Sí** | No | App Functionality, Analytics |
| Identifiers > Device ID | ID de instalación de Firebase, token de Cloud Messaging, UUID de instalación de Crashlytics | Crashlytics, Remote Config, Cloud Messaging | **Sí** | No | App Functionality |
| Usage Data > Product Interaction | `paywall_trigger` y `batch_size` | RevenueCat | **Sí** | No | Analytics |
| Usage Data > Other Usage Data | `gallery_size` (tramo) y `use_case` (respuesta opcional) | RevenueCat | **Sí** | No | Analytics |
| Diagnostics > Crash Data | Informes de cierres y errores | Crashlytics | **Sí** | No | App Functionality |
| Diagnostics > Other Diagnostic Data | Modelo del dispositivo, versión del sistema y estado de la app al fallar | Crashlytics | **Sí** | No | App Functionality |

Notas:
- **`use_case` y la "divulgación opcional":** no cumple las cuatro condiciones de Apple (entre otras,
  que el nombre del usuario aparezca en el formulario), así que hay que declararlo.
- **Clasificación de `gallery_size` y `use_case`:** "Other Usage Data" es criterio mío; también es
  defendible meter los cuatro atributos en "Product Interaction". Lo importante es que estén
  declarados con la finalidad Analytics.
- **Performance Data:** la etiqueta actual lo declara ("errores y rendimiento"), pero la documentación
  de Firebase no dice que Crashlytics recoja rendimiento (tiempo de arranque, bloqueos, consumo) y la
  app no usa Firebase Performance. Recomiendo quitarlo. Ver C4.
- **No se declaran:** ubicación (Remote Config usa el código de país de los ajustes del teléfono, no la
  ubicación), contactos, fotos o vídeos (no salen del teléfono) ni información de contacto.
- **Sin finalidad "Developer's Advertising or Marketing"** para el ID de dispositivo, porque las
  notificaciones no son promocionales (decisión de Anibal). Si algún día se envían promociones, hay que
  añadirla.
- **Comprobar en el panel de RevenueCat** [VERIFICAR] que no hay integraciones activas con terceros
  (Meta, Adjust, AppsFlyer, etc.). Si las hay, puede haber rastreo y "datos compartidos".

### 4.2 Formulario de seguridad de datos de Google Play recomendado (Play Console > Contenido de la app > Seguridad de los datos)

**Preguntas generales**

| Pregunta | Respuesta | Fuente |
|---|---|---|
| ¿Tu app recoge o comparte alguno de los tipos de datos de usuario obligatorios? | **Sí** | Google: los datos seudónimos deben declararse (*"User data collected pseudonymously must be disclosed"*) |
| ¿Todos los datos se cifran en tránsito? | **Sí** | Firebase: *"Firebase encrypts the data in transit using HTTPS"*; RevenueCat: *"RevenueCat encrypts data in transit"* |
| ¿Ofreces una forma de pedir el borrado de los datos? | **Sí**, con la URL de la página del apartado 3 | Google no exige un mecanismo concreto; RevenueCat permite borrar al cliente desde el panel o la API |
| ¿Se comparten datos con terceros? | **No** en todos los tipos: RevenueCat y Google actúan como proveedores de servicios (encargados), algo que Google no considera "compartir" | Google, definición de "sharing" y excepción de proveedores |

**Tipos de datos**

| Categoría > tipo | Qué es en iSIMILAR | SDK | Recogido | Compartido | Efímero | ¿Obligatorio u opcional? | Finalidades |
|---|---|---|---|---|---|---|---|
| Información financiera > Historial de compras | Compras y suscripción | RevenueCat | Sí | No | No | Obligatorio | Funcionalidad de la app, Análisis (lo que pide RevenueCat) |
| Actividad en la app > Interacciones con la app | `paywall_trigger`, `batch_size`, `gallery_size` | RevenueCat | Sí | No | No | Obligatorio | Análisis |
| Actividad en la app > Otras acciones | `use_case`: respuesta a un diálogo opcional | RevenueCat | Sí | No | No | **Opcional** | Análisis |
| Información y rendimiento de la app > Registros de fallos | Informes de cierres | Crashlytics | Sí | No | No | Obligatorio | Funcionalidad de la app, Análisis |
| Información y rendimiento de la app > Diagnóstico | Modelo, versión del sistema y estado de la app al fallar | Crashlytics | Sí | No | No | Obligatorio | Funcionalidad de la app, Análisis |
| Dispositivo u otros IDs | ID de instalación de Firebase (Remote Config, Cloud Messaging, Crashlytics), token de Cloud Messaging e ID de usuario de RevenueCat | Firebase, RevenueCat | Sí | No | No | Obligatorio | Funcionalidad de la app, Análisis, **Comunicaciones del desarrollador** (por Cloud Messaging) |

Notas:
- **Cloud Messaging** entra por "Dispositivo u otros IDs", con la finalidad "Comunicaciones del
  desarrollador" (Google: *"Used to send news or notifications about the app or the developer"*). Con
  notificaciones no promocionales no hay que marcar "Publicidad o marketing".
- **Remote Config** entra por "Dispositivo u otros IDs" (ID de instalación). El país, el idioma, la zona
  horaria y la versión del sistema no son tipos de datos del formulario. Si el país se dedujera de la IP
  podría contar como ubicación aproximada: Firebase habla del *"device's country code"*, que interpreto
  como el de los ajustes. [VERIFICAR]
- **No se declaran:** Fotos y vídeos. Google considera "recogido" solo lo que sale del dispositivo, y el
  análisis es local.
- **Público objetivo (Play Console):** con la edad mínima de 14 años, no marcar franjas por debajo de 13
  para no entrar en la política de familias. Qué franjas marcar exactamente lo decide Anibal [DECIDIR].

---

## 5. Lo que requiere abogado [ABOGADO]

Ordenado por riesgo.

| # | Tema | Por qué | Pregunta concreta |
|---|---|---|---|
| 1 | **Consentimiento ePrivacy (art. 122 del Codice privacy) para algo más que Analytics** | El motivo para dejar fuera Firebase Analytics puede aplicarse igual a los atributos de medición de RevenueCat (`gallery_size` se calcula a partir de la galería), a Crashlytics y al token de Cloud Messaging, que se crea antes de pedir el permiso. Las Directrices 2/2023 del CEPD (versión final del 7-10-2024) interpretan el art. 5.3 de forma amplia. Las directrices del Garante de 2021 sobre cookies admiten la analítica sin consentimiento solo con condiciones estrictas (estadística agregada, sin cruce con otros datos), y en 2026 hay comentarios que dicen que ese criterio está "sotto pressione". | ¿Pueden enviarse `paywall_trigger`, `batch_size`, `gallery_size` y los informes de Crashlytics sin consentimiento previo? ¿Debe desactivarse la creación automática del token de FCM hasta que el usuario acepte las notificaciones? |
| 2 | Bases jurídicas y prueba de ponderación | Para el interés legítimo hace falta una evaluación documentada (art. 5.2, responsabilidad proactiva). | ¿`use_case` con consentimiento o con interés legítimo? ¿Es suficiente la ponderación para los atributos de medición? |
| 3 | Transferencias a EE. UU. | RevenueCat usa cláusulas contractuales tipo (módulo 2) y Google, el Marco de Privacidad de Datos. Falta confirmar que los contratos están aceptados: el DPA de RevenueCat en su panel y los Data Processing and Security Terms de Firebase en la consola, con el contacto de privacidad rellenado. | ¿Hace falta una evaluación de impacto de la transferencia para RevenueCat? |
| 4 | Plazos de conservación | RevenueCat guarda los datos mientras dure el contrato; hay que fijar uno propio y aplicarlo. | ¿Son razonables 3 años desde la última actividad para RevenueCat y 24 meses para los correos? ¿Obliga algo la norma fiscal sobre datos por usuario? Los registros contables, 10 años según el art. 2220 del Codice civile, son los informes de venta de las tiendas, no los datos de RevenueCat. |
| 5 | Datos del responsable en la web | Ver tabla 1.0. | ¿Se puede publicar un domicilio profesional? ¿Hay inscripción en el REA? ¿Coinciden con los datos de comerciante de la App Store? |
| 6 | Menores | 14 años es la edad para dar consentimiento a servicios de la sociedad de la información (Codice privacy art. 2-quinquies); la capacidad para contratar una suscripción es otra cuestión. | ¿Hay que añadir la frase sobre autorización de los padres para compras de menores de 18? |
| 7 | Desistimiento y reembolsos | Codice del Consumo art. 59, letra o (contenido digital) y papel de Apple y Google como vendedores o comisionistas. | ¿Basta "los reembolsos los gestiona la tienda y no afecta a tus derechos"? |
| 8 | Responsabilidad, garantía legal de conformidad del contenido digital (Codice del Consumo, arts. 135-octies y siguientes) y ley aplicable (Roma I art. 6; fuero del consumidor) | Las cláusulas de los términos antiguos ("as is", tope de 12 meses, indemnización) probablemente son nulas frente a consumidores. | Revisar los apartados 11 y 13 de los términos. |
| 9 | Términos propios frente al EULA estándar de Apple | Si se usa un EULA propio, Apple exige unos términos mínimos. | ¿Mantenemos el EULA estándar de Apple y estos términos como complemento? |
| 10 | Registro de actividades de tratamiento (art. 30) | La excepción para menos de 250 empleados no se aplica si el tratamiento no es ocasional, y este es continuo. | ¿Hace falta el registro? Probablemente sí, y es sencillo. |
| 11 | Idioma que prevalece | Hay tres versiones. | ¿Añadir "en caso de discrepancia, prevalece la versión italiana o inglesa"? |
| 12 | Cookies o analítica en la web isimilar.app | La política cubre la app, no la web. | Si la web nueva usa analítica o cookies no técnicas, necesita su propio aviso. |

---

## 6. Qué tiene que estar resuelto antes de publicar la próxima versión de la app

**Bloqueantes**

| # | Qué | Dónde | Por qué |
|---|---|---|---|
| 1 | Quitar `firebase_analytics` de `pubspec.yaml:51`, el import y `AnalyticsService.init()` de `main.dart:22`, y vaciar `_log()` en `analytics_service.dart` | Sesión en `solopila/` | Si el SDK va dentro, recoge eventos automáticos que la política no declara. Ver C1. |
| 2 | Respuesta del abogado al punto 1 del apartado 5 (consentimiento para los atributos de RevenueCat, Crashlytics y el token de FCM) | Abogado | Si hace falta consentimiento, cambia la app (pantalla de aceptación) y la política. |
| 3 | Rellenar `[NOMBRE COMPLETO]`, `[DIRECCIÓN]`, `[P. IVA]` y `[EMAIL DE CONTACTO]`, crear y probar el buzón, y fijar los plazos `[DECIDIR]` | Anibal | Sin responsable identificado, la política no cumple el art. 13. |
| 4 | Publicar los textos nuevos **antes o el mismo día** en que la versión llegue a la tienda: o en isimilar.app, o sustituyendo el contenido de las 3 páginas de Notion (las versiones instaladas siguen abriendo Notion) | Web / Notion | La versión nueva envía los atributos de RevenueCat; la política tiene que decirlo antes de que ocurra. |
| 5 | Actualizar la etiqueta de App Store (4.1) y el formulario de Google Play (4.2) | App Store Connect / Play Console | Google: *"Your Data safety form responses must remain accurate and complete at all times."* Apple: respuestas exactas y actualizadas. Se puede hacer antes de enviar la versión. |
| 6 | Corregir el precio de respaldo `$12.99` | `premium_service.dart:84-91`, `premium_offer_sheet.dart` | Riesgo de mostrar un precio distinto del que se cobra. Ver C3. |
| 7 | Comprobar en un Android real que el muro de pago muestra la prueba de 7 días y el precio después de la prueba | Sesión en `solopila/` | `premium_service.dart:78-81` detecta la prueba con `introductoryPrice`. No puedo confirmar que en Google Play la prueba gratuita llegue por ese campo y no solo por las opciones de suscripción. Google: *"Offers that do not clearly explain how long the free trial … will last"* son una infracción. [VERIFICAR] |

**Recomendados (no bloquean, reducen riesgo)**

| # | Qué | Por qué |
|---|---|---|
| 8 | Cambiar las 5 URL de Notion de la app por las de isimilar.app (privacidad, términos y borrado, según el idioma) | Textos indexables y bajo tu dominio; Notion queda como redirección. |
| 9 | Añadir en la pregunta `use_case` una línea del tipo "Opcional. Se guarda con tus datos de compra. Política de privacidad" | Si la base es el consentimiento, el usuario tiene que saber qué acepta. Hoy solo dice "One quick question to improve the app." |
| 10 | Desactivar la creación automática del token de FCM hasta que se acepten las notificaciones | Coherencia con "solo si permites las notificaciones" y con el punto 1 del apartado 5. |
| 11 | Revisar que `recordError` (`scan_isolate_service.dart:257`) no envíe rutas de archivo o nombres de fotos en el texto del error | La política dice que no sale contenido de la galería; un nombre de archivo en un error es un dato de la galería. |
| 12 | Que el muro de pago siga enlazando términos y privacidad y tenga "Restaurar compras" | Apple, página de suscripciones; verificado en el borrador anterior (`premium_offer_sheet.dart:860-927`), sin volver a comprobar. |
| 13 | Ficha de App Store: URL de la política y enlace a los términos (o al EULA) en la descripción de los 3 idiomas | Apple: *"your app and App Store metadata must include links to your Terms of Use and Privacy Policy"*. |
| 14 | Pasar `checklist-release` antes de enviar | Regla del agente. |
| 15 | Fuera de alcance, sin verificar: permisos `SCHEDULE_EXACT_ALARM` y `READ_MEDIA_IMAGES` en `AndroidManifest.xml:12,18` y las políticas de Google Play sobre alarmas exactas y acceso a fotos | El código programa con `inexactAllowWhileIdle`, así que el permiso de alarma exacta podría sobrar. |

---

## 7. Contradicciones detectadas

⚠️ Contradicción detectada (C1)
- Documento: `docs/definicion-tecnica.md` · "Arquitectura" (línea 22) y "Medición" (línea 109) dice: Firebase Analytics está "fuera de la app hasta resolver el consentimiento en la UE"; "la próxima versión se publica sin la dependencia `firebase_analytics` y con esos métodos vacíos". `docs/brief-marketing.md` · línea 153 dice lo mismo.
- Fuente: `solopila/pubspec.yaml · línea 51` incluye `firebase_analytics: ^12.6.0`; `lib/main.dart · línea 22` ejecuta `AnalyticsService.init()` (activa el modo de consentimiento con `analyticsStorageConsentGranted: true`); `lib/services/analytics_service.dart · líneas 139-188` siguen enviando eventos con `logEvent`.
- Impacto: si se compila tal cual, la versión envía datos a Firebase Analytics (incluidos los eventos automáticos del SDK) sin que la política, la etiqueta ni el formulario lo declaren. Es riesgo de incumplir el art. 13 del RGPD y de rechazo o retirada en las tiendas. No puedo confirmar si la versión publicada (1.1.6+28) ya incluye el SDK.
- Opciones: A) ajustar la fuente al documento (quitar la dependencia, el import, `init()` y vaciar `_log()`) · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada (C2)
- Documento: `docs/definicion-tecnica.md` · "Datos y privacidad" (línea 76) dice: "Etiqueta de privacidad actual en la App Store: datos no vinculados a la persona". `docs/guia-estrategica.md` · "Prioridades" (línea 202) dice que hay que publicar en la web que la etiqueta declara datos "no vinculados a la persona y sin publicidad".
- Fuente: Apple, developer.apple.com/app-store/app-privacy-details, sección "Data linked to the user": *"'Personal Information' and 'Personal Data', as defined under relevant privacy laws, are considered linked to the user."* Y `definicion-tecnica.md` · línea 82: "para el RGPD son datos seudónimos, no anónimos".
- Impacto: la etiqueta actual es probablemente inexacta según la definición de Apple. Si se aplica la recomendación del apartado 4, la frase de la guía (línea 202) para la web quedaría desfasada. Cambiar a "vinculados" no implica rastreo ni publicidad.
- Opciones: A) ajustar la fuente al documento (mantener "no vinculados", con el riesgo descrito en 4.0) · B) Anibal revisa el documento: cerrar el pendiente de la línea 78 con "vinculados, sin rastreo" y cambiar en la guía (línea 202) "no vinculados a la persona y sin publicidad" por "sin rastreo y sin publicidad". **Recomiendo B.**
- Esperando decisión.

⚠️ Contradicción detectada (C3)
- Documento: `docs/definicion-tecnica.md` · "Modelo comercial en el código" (línea 56) dice: PRO cuesta 11,99 USD en EE. UU. `docs/brief-marketing.md` · "Precio" (línea 83) dice: el precio debe ser el mismo en la app, la ficha, la web y cualquier material.
- Fuente: `solopila/lib/services/premium_service.dart · líneas 84-85 y 90-91` usa `'$12.99'` y `12.99` como precio de respaldo si la tienda no responde.
- Impacto: el muro de pago puede mostrar un precio distinto del que se cobra y del que dicen los términos nuevos. Apple exige que el importe que se cobra sea el elemento de precio más destacado y correcto ("Billing amount"); Google, que el coste se indique de forma clara.
- Opciones: A) ajustar la fuente al documento (sin precio fijo; si la tienda no devuelve precio, desactivar el botón de compra y mostrar un error) · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada (C4)
- Documento: `docs/definicion-tecnica.md` · "Datos y privacidad" (líneas 69-71) dice: Crashlytics recibe "Errores y datos de rendimiento"; Cloud Messaging, "Un token del dispositivo"; Remote Config, "Un identificador de instalación".
- Fuente: firebase.google.com/docs/ios/app-store-data-collection y firebase.google.com/docs/android/play-data-disclosure dicen: Cloud Messaging también recoge *"device model, language, time zone, OS version, application identifier and application version"* (iOS); Remote Config, *"country code, language code, time zone, OS version"* y los identificadores de la app; Crashlytics, trazas, estado de la app y datos del dispositivo, **sin mencionar datos de rendimiento**.
- Impacto: bajo. La política nueva es más detallada que el documento (lo cual es correcto según el art. 13) y la etiqueta recomendada quita "Performance Data". Si alguien redacta textos solo a partir del documento, saldrán incompletos.
- Opciones: A) ajustar la fuente al documento (no aplica: la fuente es la documentación de Google) · B) Anibal revisa el documento para completar las tres filas
- Esperando decisión.

**No es contradicción, pero hay que saberlo:**
- La petición mencionaba los atributos `use_case` y `paywall_trigger`. El documento (líneas 90-95) y el código (`analytics_service.dart:87-116`) envían también `batch_size` y `gallery_size`. La política incluye los cuatro; si faltara alguno, estaría incompleta.
- `use_case` también se registra como evento de Analytics (`analytics_service.dart:117`). Con el punto C1 resuelto, no sale.
- La decisión "notificaciones: solo avisos de la app y de versiones nuevas" es compatible con el recordatorio semanal opcional del documento (línea 31), que es una notificación local que no envía datos. La política lo dice así.

---

## 8. Fuentes oficiales consultadas (22-10-2026)

- Apple App Review Guidelines 3.1.1, 3.1.2(a), 3.1.2(c), 5.1.1(i), 5.1.1(v), 5.1.2(i): https://developer.apple.com/app-store/review/guidelines/
- Apple, App Privacy Details: https://developer.apple.com/app-store/app-privacy-details/
- Apple, Auto-renewable subscriptions ("Clearly describing subscriptions", "Billing amount", "Free trials"): https://developer.apple.com/app-store/subscriptions/
- Apple, StoreKit "Handling Subscriptions Billing": https://developer.apple.com/documentation/storekit/handling-subscriptions-billing
- Apple Support, cancelar una suscripción: https://support.apple.com/en-us/118428
- Google Play, Seguridad de los datos: https://support.google.com/googleplay/android-developer/answer/10787469
- Google Play, política de suscripciones: https://support.google.com/googleplay/android-developer/answer/9900533
- Google Play Help, cancelar una suscripción: https://support.google.com/googleplay/answer/7018481
- Firebase, datos para la App Store: https://firebase.google.com/docs/ios/app-store-data-collection
- Firebase, datos para Google Play: https://firebase.google.com/docs/android/play-data-disclosure
- Firebase, privacidad (conservación, Marco de Privacidad de Datos, encargado del tratamiento): https://firebase.google.com/support/privacy
- RevenueCat, Apple App Privacy: https://www.revenuecat.com/docs/platform-resources/apple-platform-resources/apple-app-privacy
- RevenueCat, Google Play Data Safety: https://www.revenuecat.com/docs/platform-resources/google-platform-resources/google-plays-data-safety
- RevenueCat, DPA (cláusulas contractuales tipo, subencargados): https://www.revenuecat.com/dpa
- RevenueCat, blog sobre la etiqueta con IDs anónimos: https://www.revenuecat.com/blog/engineering/privacy-focused-subscriptions-in-your-swift-app
- CEPD, Directrices 2/2023 sobre el art. 5.3 de ePrivacy (final, v2.0): https://www.edpb.europa.eu/documents/530_en (no he leído el texto completo sobre SDK de apps)
- Normativa italiana, a través de fuentes secundarias (verificar en Normattiva): DPR 633/1972 art. 35 (P. IVA en la web), D.Lgs. 70/2003 art. 7, Codice privacy arts. 2-quinquies y 122, directrices del Garante sobre cookies (2021).
