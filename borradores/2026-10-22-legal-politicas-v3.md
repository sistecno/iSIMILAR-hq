# iSIMILAR · Textos legales v3: privacidad, términos, borrado de datos, etiquetas y muro de pago

Fecha: 2026-10-22 · Autor: legal-tiendas · Estado: BORRADOR para publicar tras rellenar los marcadores.
Sustituye a `borradores/2026-10-22-legal-politicas-v2.md`, que se queda como está.
Base: decisiones de Anibal del 22-10 y `docs/definicion-tecnica.md` · "Datos y privacidad", releído hoy
(Crashlytics solo con informes de errores; token de Cloud Messaging solo al activar el recordatorio;
decisión sobre la etiqueta; párrafo de consentimiento).

> No es asesoramiento legal. Se publica sin revisión de abogado por decisión de Anibal; los riesgos
> que eso supone están en el apartado 7 y la revisión futura recomendada, en el anexo A.

**Marcadores que quedan en los textos publicables (se rellenan a mano)**
- `[NOMBRE]`, `[P. IVA]`, `[DIRECCIÓN]`, `[EMAIL]`. Sugerencia para `[EMAIL]`: info@isimilar.app.
- `[REA si aplica]`: el número REA solo si estás inscrito en el Registro delle Imprese; si no, borra la línea entera.
- `[FECHA]`: el día de publicación.

Las URL propuestas son `https://isimilar.app/privacy`, `/terms` y `/delete-data`, con `/es/…` y `/it/…`.
Si se publican en otra dirección, hay que cambiarlas en los textos.

---

## 0. Antes de publicar: condiciones para que el texto sea cierto

La política describe la app como debe quedar según las decisiones del 22-10. **El código actual todavía
no coincide en dos puntos.** Si se publica esta política con el código de hoy, la política es falsa.

| # | Qué falta | Dónde | Estado |
|---|---|---|---|
| 1 | Quitar `firebase_analytics` (`pubspec.yaml:51`) y `AnalyticsService.init()` (`main.dart:22`) | `solopila/` | **No cumple.** Ver C1 |
| 2 | Que el token de Cloud Messaging se cree solo al activar el recordatorio y aceptar el permiso | `solopila/` | **No cumple.** Ver C5 |
| 3 | Borrar el token al desactivar el recordatorio (`FirebaseMessaging.instance.deleteToken()`) | `solopila/` | No existe. La política lo promete en la sección 5 |
| 4 | Corregir el precio de respaldo `$12.99` | `premium_service.dart:84-91` | **No cumple.** Ver C3 |
| 5 | Rellenar los marcadores, crear el buzón y publicar las 3 páginas (o pegar el texto en Notion) antes o el mismo día que salga la versión | Web / Notion | Pendiente |
| 6 | Etiqueta de App Store (apartado 4.1) y formulario de Google Play (apartado 4.2) | Consolas | Pendiente |

---

## 1. Política de privacidad

### 1.1 Privacy Policy (EN)

```
# iSIMILAR Privacy Policy

Last updated: [FECHA]

This policy explains what data the iSIMILAR app uses, what leaves your phone and why, and
what rights you have. It applies to the iSIMILAR app for iOS and Android.

## 1. The short version

- Your photos never leave your phone. Your photos, the thumbnails used to analyse them
  and the visual vectors the app calculates are created, stored and searched only on your
  device.
- There is no account. We never ask for your name, email address or phone number.
- To sell and manage the subscription, fix errors, check for required updates and, if you
  turn them on, send notifications, the app sends technical data about purchases, usage
  and errors to the providers listed in section 5. This data never includes your photos or
  the content of your gallery.
- That data is linked to random identifiers, not to your name. Under the EU General Data
  Protection Regulation (GDPR) it is pseudonymous personal data, not anonymous data, and
  this policy treats it as personal data.
- We do not show ads, we do not track you across other companies' apps or websites, we do
  not collect the advertising identifier (IDFA on iOS, Advertising ID on Android) and we
  do not sell your data.

## 2. Who is responsible for your data

Data controller: [NOMBRE], self-employed, established in Italy
Address: [DIRECCIÓN]
VAT number (P. IVA): [P. IVA]
[REA si aplica]
Email: [EMAIL]

[NOMBRE] is also the seller of iSIMILAR on the App Store and Google Play. We have not
appointed a Data Protection Officer because the law does not require one for this
activity.

## 3. What stays on your phone

- Your photos and your albums.
- 224-pixel thumbnails the app creates temporarily to analyse each photo.
- The visual vectors (lists of numbers that describe what a photo looks like) and the
  search index, stored in a local database on your phone.
- The photo you take with the camera to search.
- Your app settings, such as language and notification preferences.

The visual analysis runs entirely on your phone and works without an internet
connection. None of this is sent to us or to anyone else. It is deleted when you use
Settings > Reset App or uninstall the app.

## 4. Permissions the app asks for

- Photos: required. To scan and search your gallery on your phone and, only when you
  confirm it, to delete, move or share photos.
- Camera: optional. To take a photo and use it as a search.
- Notifications: optional. Only if you turn on the weekly reminder (section 5.4).

You can change these permissions at any time in your phone's settings.

## 5. What leaves your phone, service by service

Each provider acts on our behalf as a data processor under a data processing agreement
and must protect your data at least to the level described in this policy. None of them
receives your photos, thumbnails, vectors, the photo you take with the camera or any
other content of your gallery.

### 5.1 RevenueCat (RevenueCat, Inc., United States): purchases

What it receives:
- Your purchase and subscription information: product, dates, price, currency, store,
  trial and renewal status.
- A random user ID created by RevenueCat when you first open the app. It is not your
  name, email or Apple or Google account.
- Basic technical data: app version, operating system, and language and region settings.

Why: to process, validate and restore your subscription.
Legal basis: performance of the contract you enter into when you subscribe
(Art. 6(1)(b) GDPR).
Retention: while your subscription is active and for 3 years after your last activity,
unless you ask us to delete it earlier.
How to object: this data is needed to provide the subscription. You can ask us to delete
it (section 9); if you then use Restore Purchases, a new record is created so you keep
PRO.

### 5.2 RevenueCat: measurement fields

What it receives, linked to the same random user ID:
- paywall_trigger: what opened the PRO screen (a camera search, a batch delete, a batch
  move to an album, or the button in Settings).
- batch_size: how many photos you had selected when the PRO screen opened from a batch
  action.
- gallery_size: the size of your gallery as a range (under 3,000, 3,000 to 10,000, or
  over 10,000 photos). Sent once, after the first scan.
- use_case: only if you choose to answer the optional question shown after a purchase or
  after a free trial starts: what you mainly use iSIMILAR for (repair and technical
  service; construction, installations or inspections; a portfolio; another type of
  work; cleaning up memes and screenshots; products, shopping and everyday photos; or
  something else). You can skip it.

Why: to understand which features lead people to choose PRO and what they use the app
for, so we can improve it.
Legal basis: for paywall_trigger, batch_size and gallery_size, our legitimate interest in
improving the app with a small set of data that never includes your photos
(Art. 6(1)(f) GDPR). For use_case, your consent, given by choosing to answer
(Art. 6(1)(a)).
Retention: same as section 5.1.
How to object or withdraw consent: email us with your iSIMILAR ID (section 9) and we will
delete these fields. The app may record new ones the next time the PRO screen opens; if
you ask, we will delete those too.

### 5.3 Firebase Crashlytics (Google): error reports

What it receives: when the app crashes or hits an error, a report with technical details
of the error and the state of the app at that moment, device model, operating system
version and app version, linked to an installation identifier. It is not linked to your
iSIMILAR ID.

Why: to find and fix errors and keep the app stable and secure.
Legal basis: our legitimate interest in the stability and security of the app
(Art. 6(1)(f) GDPR).
Retention: 90 days; Google then starts removing reports from its systems (source:
firebase.google.com/support/privacy).
How to object: email us. Because error reports are not linked to your iSIMILAR ID, we
cannot pick out yours; reports stop when you uninstall the app and are deleted after 90
days.

### 5.4 Firebase Cloud Messaging (Google): notifications

What it receives: only if you turn on the weekly reminder and allow notifications, a
notification token linked to a Firebase installation identifier, together with device
model, language, time zone, operating system version and app version. If you do not turn
on the reminder, no token is created.

Why: to send you notices about the app and about new versions. We never send promotional
or advertising notifications. The weekly reminder itself is created on your phone and
sends no data.
Legal basis: your consent, given when you turn on the reminder and accept the
notification permission (Art. 6(1)(a) GDPR).
Retention: when you turn off the reminder, the app deletes the token. Otherwise Google
treats a token as expired after 270 days without activity on Android (source:
firebase.google.com/docs/cloud-messaging/manage-tokens).
How to withdraw consent: turn off the weekly reminder in the app's Settings, or turn off
notifications for iSIMILAR in your phone's settings.

### 5.5 Firebase Remote Config (Google): required updates

What it receives: country and language settings, time zone, operating system version and
app identifiers, linked to a Firebase installation identifier.

Why: to know the minimum app version that still works and, if yours is older, to ask you
to update. This check is technically necessary for the app to work safely.
Legal basis: our legitimate interest in keeping the app working and secure
(Art. 6(1)(f) GDPR).
Retention: Google keeps the installation identifier until it is deleted, and removes
deleted identifiers from its systems within 180 days (source:
firebase.google.com/support/privacy).
How to object: email us. The app cannot work safely without this check, so the only way
to stop it completely is to uninstall the app.

### 5.6 Payments

Payments are processed by Apple (App Store) or Google (Google Play) under their own terms
and privacy policies. We never see your card or bank details; we only receive the status
of your purchase through RevenueCat. Apple and Google keep their own purchase records.

### 5.7 Emails you send us

If you write to us, we use your email address and message to answer you, based on our
legitimate interest in replying and, for privacy requests, our legal obligation
(Art. 6(1)(f) and 6(1)(c) GDPR). We keep them for 24 months after the last message.

## 6. International transfers

RevenueCat and Google may process data in the United States.
- RevenueCat, Inc.: the European Commission's Standard Contractual Clauses, included in
  RevenueCat's data processing agreement.
- Google LLC (Firebase): Google is certified under the EU-U.S. Data Privacy Framework;
  Firebase's terms also include the Standard Contractual Clauses.

These providers use their own sub-processors, bound by the same obligations. You can ask
us for a copy of these safeguards.

## 7. Your rights

You can ask us to access your data, correct it, delete it, restrict its processing,
receive a copy of it, and object to processing based on legitimate interest
(Arts. 15 to 21 GDPR). Where processing is based on consent, you can withdraw it at any
time without affecting what was done before.

Because there is no account, we need your iSIMILAR ID to find your data in RevenueCat
(section 9). Error reports and Firebase identifiers are not linked to that ID, so we
cannot identify which ones are yours (Art. 11 GDPR); the retention periods above still
apply.

We will answer within one month. You can also lodge a complaint with the Italian data
protection authority, the Garante per la protezione dei dati personali
(www.garanteprivacy.it), or with the authority of the EU country where you live or work.

## 8. On your phone

Settings > Reset App deletes the visual index and the analysis data. Uninstalling the
app deletes everything the app stores on your phone. Your photos are not deleted in
either case.

## 9. Deleting your data and contacting us

Step-by-step instructions: https://isimilar.app/delete-data

In short: open Settings in the app, press and hold the version number to copy your
iSIMILAR ID, and email it to [EMAIL] with the subject "Delete my data". Deleting your data
does not cancel your subscription; see the Terms of Use.

## 10. Age

You must be at least 14 years old, or the minimum age required by the laws of your
country if higher, to use iSIMILAR.

We do not knowingly collect data from anyone below that age. If you think this has
happened, write to us and we will delete it.

## 11. Automated decisions

We do not make decisions about you based solely on automated processing, and we do not
build advertising profiles.

## 12. Changes to this policy

If we change how the app uses data, we will update this page and the date above before
the change reaches the app. If the change is significant, we will also tell you in the
app.

## 13. Contact

[EMAIL]
```

### 1.2 Política de privacidad (ES)

```
# Política de privacidad de iSIMILAR

Última actualización: [FECHA]

Esta política explica qué datos usa la app iSIMILAR, qué sale de tu teléfono y para qué, y
qué derechos tienes. Se aplica a la app iSIMILAR para iOS y Android.

## 1. En resumen

- Tus fotos nunca salen del teléfono. Tus fotos, las miniaturas que se usan para
  analizarlas y los vectores visuales que calcula la app se crean, se guardan y se buscan
  solo en tu dispositivo.
- No hay cuentas. Nunca te pedimos nombre, correo ni teléfono.
- Para vender y gestionar la suscripción, corregir errores, comprobar si hace falta
  actualizar y, si las activas, enviarte notificaciones, la app envía datos técnicos de
  compras, uso y errores a los proveedores del apartado 5. Esos datos nunca incluyen tus
  fotos ni el contenido de tu galería.
- Esos datos van asociados a identificadores aleatorios, no a tu nombre. Según el
  Reglamento General de Protección de Datos (RGPD) son datos personales seudónimos, no
  anónimos, y esta política los trata como datos personales.
- No mostramos publicidad, no te rastreamos en apps ni webs de otras empresas, no
  recogemos el identificador publicitario (IDFA en iOS, ID de publicidad en Android) y no
  vendemos tus datos.

## 2. Responsable de tus datos

Responsable del tratamiento: [NOMBRE], trabajador autónomo establecido en Italia
Dirección: [DIRECCIÓN]
P. IVA: [P. IVA]
[REA si aplica]
Correo: [EMAIL]

[NOMBRE] es también quien vende iSIMILAR en la App Store y en Google Play. No hemos
designado un delegado de protección de datos porque la ley no lo exige para esta
actividad.

## 3. Qué se queda en tu teléfono

- Tus fotos y tus álbumes.
- Las miniaturas de 224 píxeles que la app crea de forma temporal para analizar cada foto.
- Los vectores visuales (listas de números que describen cómo es una foto) y el índice de
  búsqueda, guardados en una base de datos local de tu teléfono.
- La foto que haces con la cámara para buscar.
- Los ajustes de la app, como el idioma y las preferencias de notificaciones.

El análisis visual se hace por completo en tu teléfono y funciona sin conexión a internet.
Nada de esto se envía a nosotros ni a nadie. Se borra con Ajustes > Restablecer App o al
desinstalar la app.

## 4. Permisos que pide la app

- Fotos: necesario. Para escanear y buscar en tu galería dentro del teléfono y, solo
  cuando lo confirmas, para borrar, mover o compartir fotos.
- Cámara: opcional. Para hacer una foto y usarla como búsqueda.
- Notificaciones: opcional. Solo si activas el recordatorio semanal (apartado 5.4).

Puedes cambiar estos permisos cuando quieras en los ajustes del teléfono.

## 5. Qué sale de tu teléfono, servicio por servicio

Cada proveedor actúa por cuenta nuestra como encargado del tratamiento, con un contrato de
encargo, y debe proteger tus datos al menos con el nivel que describe esta política.
Ninguno recibe tus fotos, las miniaturas, los vectores, la foto que haces con la cámara ni
ningún otro contenido de tu galería.

### 5.1 RevenueCat (RevenueCat, Inc., Estados Unidos): compras

Qué recibe:
- La información de tu compra y tu suscripción: producto, fechas, precio, moneda, tienda
  y estado de la prueba y de la renovación.
- Un identificador de usuario aleatorio que RevenueCat crea la primera vez que abres la
  app. No es tu nombre, tu correo ni tu cuenta de Apple o Google.
- Datos técnicos básicos: versión de la app, sistema operativo y ajustes de idioma y
  región.

Para qué: gestionar, validar y restaurar tu suscripción.
Base legal: ejecución del contrato que aceptas al suscribirte (art. 6.1.b RGPD).
Conservación: mientras tu suscripción esté activa y durante 3 años desde tu última
actividad, salvo que nos pidas borrarlos antes.
Cómo oponerte: estos datos son necesarios para prestar la suscripción. Puedes pedirnos que
los borremos (apartado 9); si después usas "Restaurar compras", se crea un registro nuevo
para que mantengas PRO.

### 5.2 RevenueCat: campos de medición

Qué recibe, asociado al mismo identificador aleatorio:
- paywall_trigger: qué abrió la pantalla de PRO (una búsqueda con la cámara, un borrado en
  lote, mover en lote a un álbum o el botón de Ajustes).
- batch_size: cuántas fotos tenías seleccionadas cuando la pantalla de PRO se abrió desde
  una acción en lote.
- gallery_size: el tamaño de tu galería por tramos (menos de 3.000, de 3.000 a 10.000 o
  más de 10.000 fotos). Se envía una sola vez, tras el primer escaneo.
- use_case: solo si decides responder a la pregunta opcional que aparece después de una
  compra o del inicio de una prueba gratuita: para qué usas sobre todo iSIMILAR
  (reparación y servicio técnico; obras, instalaciones o inspecciones; un portfolio; otro
  tipo de trabajo; limpiar memes y capturas; productos, compras y fotos del día a día; u
  otra cosa). Puedes omitirla.

Para qué: entender qué funciones llevan a elegir PRO y para qué se usa la app, para
mejorarla.
Base legal: para paywall_trigger, batch_size y gallery_size, nuestro interés legítimo en
mejorar la app con un conjunto pequeño de datos que nunca incluye tus fotos (art. 6.1.f
RGPD). Para use_case, tu consentimiento, que das al decidir responder (art. 6.1.a).
Conservación: la misma que en el apartado 5.1.
Cómo oponerte o retirar el consentimiento: escríbenos con tu ID de iSIMILAR (apartado 9) y
borraremos estos campos. La app puede registrar campos nuevos la próxima vez que se abra
la pantalla de PRO; si nos lo pides, también los borraremos.

### 5.3 Firebase Crashlytics (Google): informes de errores

Qué recibe: cuando la app se cierra o sufre un error, un informe con los detalles técnicos
del error y el estado de la app en ese momento, el modelo del dispositivo, la versión del
sistema operativo y la versión de la app, asociado a un identificador de instalación. No
está asociado a tu ID de iSIMILAR.

Para qué: encontrar y corregir errores y mantener la app estable y segura.
Base legal: nuestro interés legítimo en la estabilidad y la seguridad de la app (art. 6.1.f
RGPD).
Conservación: 90 días; después Google empieza a borrar los informes de sus sistemas
(fuente: firebase.google.com/support/privacy).
Cómo oponerte: escríbenos. Como los informes no están asociados a tu ID de iSIMILAR, no
podemos distinguir los tuyos; dejan de enviarse al desinstalar la app y se borran a los 90
días.

### 5.4 Firebase Cloud Messaging (Google): notificaciones

Qué recibe: solo si activas el recordatorio semanal y permites las notificaciones, un
token de notificaciones asociado a un identificador de instalación de Firebase, junto con
el modelo del dispositivo, el idioma, la zona horaria, la versión del sistema operativo y
la versión de la app. Si no activas el recordatorio, no se crea ningún token.

Para qué: enviarte avisos sobre la app y sobre versiones nuevas. Nunca enviamos
notificaciones promocionales ni publicitarias. El recordatorio semanal en sí se crea en tu
teléfono y no envía ningún dato.
Base legal: tu consentimiento, que das al activar el recordatorio y aceptar el permiso de
notificaciones (art. 6.1.a RGPD).
Conservación: al desactivar el recordatorio, la app borra el token. Si no, Google da por
caducado un token tras 270 días sin actividad en Android (fuente:
firebase.google.com/docs/cloud-messaging/manage-tokens).
Cómo retirar el consentimiento: desactiva el recordatorio semanal en los Ajustes de la app
o las notificaciones de iSIMILAR en los ajustes del teléfono.

### 5.5 Firebase Remote Config (Google): actualizaciones obligatorias

Qué recibe: ajustes de país e idioma, zona horaria, versión del sistema operativo e
identificadores de la app, asociados a un identificador de instalación de Firebase.

Para qué: saber cuál es la versión mínima de la app que sigue funcionando y, si la tuya es
anterior, pedirte que actualices. Esta comprobación es técnicamente necesaria para que la
app funcione de forma segura.
Base legal: nuestro interés legítimo en que la app funcione y sea segura (art. 6.1.f
RGPD).
Conservación: Google conserva el identificador de instalación hasta que se borra, y elimina
los identificadores borrados de sus sistemas en un máximo de 180 días (fuente:
firebase.google.com/support/privacy).
Cómo oponerte: escríbenos. La app no puede funcionar de forma segura sin esta comprobación,
así que la única forma de detenerla del todo es desinstalar la app.

### 5.6 Pagos

Los pagos los procesa Apple (App Store) o Google (Google Play) según sus propios términos y
políticas de privacidad. Nunca vemos los datos de tu tarjeta ni de tu banco; solo
recibimos el estado de tu compra a través de RevenueCat. Apple y Google conservan sus
propios registros de compras.

### 5.7 Correos que nos envías

Si nos escribes, usamos tu dirección de correo y tu mensaje para responderte, por nuestro
interés legítimo en atenderte y, en las solicitudes de privacidad, por una obligación
legal (arts. 6.1.f y 6.1.c RGPD). Los conservamos 24 meses desde el último mensaje.

## 6. Transferencias internacionales

RevenueCat y Google pueden tratar datos en Estados Unidos.
- RevenueCat, Inc.: cláusulas contractuales tipo de la Comisión Europea, incluidas en su
  contrato de encargo del tratamiento.
- Google LLC (Firebase): Google está certificada en el Marco de Privacidad de Datos
  UE-EE. UU.; los términos de Firebase incluyen también las cláusulas contractuales tipo.

Estos proveedores usan a su vez subencargados sujetos a las mismas obligaciones. Puedes
pedirnos una copia de estas garantías.

## 7. Tus derechos

Puedes pedirnos acceder a tus datos, rectificarlos, borrarlos, limitar su tratamiento,
recibir una copia y oponerte al tratamiento basado en el interés legítimo (arts. 15 a 21
RGPD). Si el tratamiento se basa en el consentimiento, puedes retirarlo cuando quieras, sin
que afecte a lo hecho antes.

Como no hay cuentas, necesitamos tu ID de iSIMILAR para encontrar tus datos en RevenueCat
(apartado 9). Los informes de errores y los identificadores de Firebase no están asociados
a ese ID, así que no podemos saber cuáles son tuyos (art. 11 RGPD); aun así se les aplican
los plazos indicados arriba.

Te responderemos en el plazo de un mes. También puedes reclamar ante la autoridad italiana
de protección de datos, el Garante per la protezione dei dati personali
(www.garanteprivacy.it), o ante la autoridad del país de la UE en el que vivas o trabajes.

## 8. En tu teléfono

Ajustes > Restablecer App borra el índice visual y los datos de análisis. Desinstalar la
app borra todo lo que la app guarda en tu teléfono. En ningún caso se borran tus fotos.

## 9. Borrar tus datos y contactarnos

Instrucciones paso a paso: https://isimilar.app/es/delete-data

En resumen: abre Ajustes en la app, mantén pulsado el número de versión para copiar tu ID
de iSIMILAR y envíalo a [EMAIL] con el asunto "Borrar mis datos". Borrar tus datos no
cancela la suscripción; consulta los Términos de uso.

## 10. Edad

Debes tener al menos 14 años, o la edad mínima que exija la ley de tu país si es mayor,
para usar iSIMILAR.

No recogemos de forma consciente datos de nadie por debajo de esa edad. Si crees que ha
ocurrido, escríbenos y los borraremos.

## 11. Decisiones automatizadas

No tomamos decisiones sobre ti basadas únicamente en un tratamiento automatizado ni
creamos perfiles publicitarios.

## 12. Cambios en esta política

Si cambia el uso que la app hace de los datos, actualizaremos esta página y la fecha de
arriba antes de que el cambio llegue a la app. Si el cambio es importante, también te lo
diremos en la app.

## 13. Contacto

[EMAIL]
```

### 1.3 Informativa sulla privacy (IT)

```
# Informativa sulla privacy di iSIMILAR

Ultimo aggiornamento: [FECHA]

Questa informativa spiega quali dati usa l'app iSIMILAR, cosa esce dal tuo telefono e
perché, e quali diritti hai. Si applica all'app iSIMILAR per iOS e Android.

## 1. In breve

- Le tue foto non escono mai dal telefono. Le foto, le miniature usate per analizzarle e i
  vettori visivi calcolati dall'app vengono creati, salvati e cercati solo sul tuo
  dispositivo.
- Non esistono account. Non ti chiediamo mai nome, email o numero di telefono.
- Per vendere e gestire l'abbonamento, correggere gli errori, verificare se serve un
  aggiornamento e, se le attivi, inviarti notifiche, l'app invia dati tecnici su acquisti,
  utilizzo ed errori ai fornitori elencati nella sezione 5. Questi dati non includono mai
  le tue foto né il contenuto della galleria.
- Questi dati sono associati a identificativi casuali, non al tuo nome. Ai sensi del
  Regolamento generale sulla protezione dei dati (GDPR) sono dati personali pseudonimi,
  non anonimi, e questa informativa li tratta come dati personali.
- Non mostriamo pubblicità, non ti tracciamo su app o siti di altre aziende, non
  raccogliamo l'identificativo pubblicitario (IDFA su iOS, ID pubblicità su Android) e non
  vendiamo i tuoi dati.

## 2. Titolare del trattamento

Titolare: [NOMBRE], lavoratore autonomo stabilito in Italia
Indirizzo: [DIRECCIÓN]
P. IVA: [P. IVA]
[REA si aplica]
Email: [EMAIL]

[NOMBRE] è anche il venditore di iSIMILAR sull'App Store e su Google Play. Non abbiamo
designato un responsabile della protezione dei dati perché la legge non lo richiede per
questa attività.

## 3. Cosa resta sul tuo telefono

- Le tue foto e i tuoi album.
- Le miniature da 224 pixel che l'app crea temporaneamente per analizzare ogni foto.
- I vettori visivi (sequenze di numeri che descrivono l'aspetto di una foto) e l'indice di
  ricerca, salvati in un database locale sul telefono.
- La foto che scatti con la fotocamera per cercare.
- Le impostazioni dell'app, come la lingua e le preferenze delle notifiche.

L'analisi visiva avviene interamente sul telefono e funziona senza connessione a internet.
Niente di tutto questo viene inviato a noi o ad altri. Viene cancellato con Impostazioni >
Reimposta App o disinstallando l'app.

## 4. Autorizzazioni richieste dall'app

- Foto: necessaria. Per scansionare e cercare nella galleria sul telefono e, solo quando lo
  confermi, per eliminare, spostare o condividere foto.
- Fotocamera: facoltativa. Per scattare una foto e usarla come ricerca.
- Notifiche: facoltative. Solo se attivi il promemoria settimanale (sezione 5.4).

Puoi modificare queste autorizzazioni in qualsiasi momento dalle impostazioni del telefono.

## 5. Cosa esce dal tuo telefono, servizio per servizio

Ogni fornitore agisce per nostro conto come responsabile del trattamento, in base a un
accordo sul trattamento dei dati, ed è tenuto a proteggere i tuoi dati almeno al livello
descritto in questa informativa. Nessuno riceve le tue foto, le miniature, i vettori, la
foto che scatti con la fotocamera o qualsiasi altro contenuto della galleria.

### 5.1 RevenueCat (RevenueCat, Inc., Stati Uniti): acquisti

Cosa riceve:
- Le informazioni sull'acquisto e sull'abbonamento: prodotto, date, prezzo, valuta, store
  e stato della prova e del rinnovo.
- Un identificativo utente casuale creato da RevenueCat al primo avvio dell'app. Non è il
  tuo nome, la tua email né il tuo account Apple o Google.
- Dati tecnici di base: versione dell'app, sistema operativo e impostazioni di lingua e
  area geografica.

Perché: gestire, convalidare e ripristinare l'abbonamento.
Base giuridica: esecuzione del contratto che accetti quando ti abboni (art. 6, par. 1,
lett. b GDPR).
Conservazione: finché l'abbonamento è attivo e per 3 anni dalla tua ultima attività, salvo
che tu ci chieda di cancellarli prima.
Come opporti: questi dati sono necessari per fornire l'abbonamento. Puoi chiederci di
cancellarli (sezione 9); se poi usi "Ripristina acquisti", viene creato un nuovo record
per mantenere PRO.

### 5.2 RevenueCat: campi di misurazione

Cosa riceve, associato allo stesso identificativo casuale:
- paywall_trigger: cosa ha aperto la schermata PRO (una ricerca con la fotocamera,
  un'eliminazione multipla, uno spostamento multiplo in un album o il pulsante nelle
  Impostazioni).
- batch_size: quante foto avevi selezionato quando la schermata PRO si è aperta da
  un'azione multipla.
- gallery_size: la dimensione della galleria per fasce (meno di 3.000, da 3.000 a 10.000 o
  oltre 10.000 foto). Inviato una sola volta, dopo la prima scansione.
- use_case: solo se scegli di rispondere alla domanda facoltativa mostrata dopo un acquisto
  o dopo l'inizio di una prova gratuita: per cosa usi soprattutto iSIMILAR (riparazione e
  servizio tecnico; cantieri, installazioni o ispezioni; un portfolio; un altro tipo di
  lavoro; pulire meme e screenshot; prodotti, acquisti e foto quotidiane; oppure
  qualcos'altro). Puoi saltarla.

Perché: capire quali funzioni portano a scegliere PRO e per cosa viene usata l'app, per
migliorarla.
Base giuridica: per paywall_trigger, batch_size e gallery_size, il nostro legittimo
interesse a migliorare l'app con un insieme ridotto di dati che non include mai le tue foto
(art. 6, par. 1, lett. f GDPR). Per use_case, il tuo consenso, dato scegliendo di
rispondere (art. 6, par. 1, lett. a).
Conservazione: come nella sezione 5.1.
Come opporti o revocare il consenso: scrivici con il tuo ID iSIMILAR (sezione 9) e
cancelleremo questi campi. L'app potrebbe registrarne di nuovi la prossima volta che si
apre la schermata PRO; se ce lo chiedi, cancelleremo anche quelli.

### 5.3 Firebase Crashlytics (Google): report degli errori

Cosa riceve: quando l'app si chiude in modo anomalo o incontra un errore, un report con i
dettagli tecnici dell'errore e lo stato dell'app in quel momento, il modello del
dispositivo, la versione del sistema operativo e la versione dell'app, associato a un
identificativo di installazione. Non è associato al tuo ID iSIMILAR.

Perché: trovare e correggere gli errori e mantenere l'app stabile e sicura.
Base giuridica: il nostro legittimo interesse alla stabilità e alla sicurezza dell'app
(art. 6, par. 1, lett. f GDPR).
Conservazione: 90 giorni; poi Google inizia a cancellare i report dai suoi sistemi (fonte:
firebase.google.com/support/privacy).
Come opporti: scrivici. Poiché i report non sono associati al tuo ID iSIMILAR, non possiamo
individuare i tuoi; smettono di essere inviati quando disinstalli l'app e vengono
cancellati dopo 90 giorni.

### 5.4 Firebase Cloud Messaging (Google): notifiche

Cosa riceve: solo se attivi il promemoria settimanale e consenti le notifiche, un token per
le notifiche associato a un identificativo di installazione Firebase, insieme al modello
del dispositivo, alla lingua, al fuso orario, alla versione del sistema operativo e alla
versione dell'app. Se non attivi il promemoria, non viene creato alcun token.

Perché: inviarti avvisi sull'app e sulle nuove versioni. Non inviamo mai notifiche
promozionali o pubblicitarie. Il promemoria settimanale viene creato sul telefono e non
invia alcun dato.
Base giuridica: il tuo consenso, dato quando attivi il promemoria e accetti l'autorizzazione
alle notifiche (art. 6, par. 1, lett. a GDPR).
Conservazione: quando disattivi il promemoria, l'app cancella il token. Altrimenti Google
considera scaduto un token dopo 270 giorni di inattività su Android (fonte:
firebase.google.com/docs/cloud-messaging/manage-tokens).
Come revocare il consenso: disattiva il promemoria settimanale nelle Impostazioni dell'app o
le notifiche di iSIMILAR nelle impostazioni del telefono.

### 5.5 Firebase Remote Config (Google): aggiornamenti obbligatori

Cosa riceve: impostazioni di paese e lingua, fuso orario, versione del sistema operativo e
identificativi dell'app, associati a un identificativo di installazione Firebase.

Perché: sapere qual è la versione minima dell'app ancora funzionante e, se la tua è
precedente, chiederti di aggiornarla. Questa verifica è tecnicamente necessaria per far
funzionare l'app in modo sicuro.
Base giuridica: il nostro legittimo interesse a far funzionare l'app in modo sicuro
(art. 6, par. 1, lett. f GDPR).
Conservazione: Google conserva l'identificativo di installazione finché non viene
cancellato, e rimuove gli identificativi cancellati dai suoi sistemi entro 180 giorni
(fonte: firebase.google.com/support/privacy).
Come opporti: scrivici. L'app non può funzionare in modo sicuro senza questa verifica,
quindi l'unico modo per interromperla del tutto è disinstallare l'app.

### 5.6 Pagamenti

I pagamenti sono gestiti da Apple (App Store) o Google (Google Play) secondo i loro termini
e le loro informative. Non vediamo mai i dati della tua carta o del tuo conto; riceviamo
solo lo stato dell'acquisto tramite RevenueCat. Apple e Google conservano i propri
registri degli acquisti.

### 5.7 Email che ci invii

Se ci scrivi, usiamo il tuo indirizzo email e il messaggio per risponderti, in base al
nostro legittimo interesse a risponderti e, per le richieste sulla privacy, a un obbligo di
legge (art. 6, par. 1, lett. f e c GDPR). Li conserviamo per 24 mesi dall'ultimo
messaggio.

## 6. Trasferimenti internazionali

RevenueCat e Google possono trattare dati negli Stati Uniti.
- RevenueCat, Inc.: clausole contrattuali tipo della Commissione europea, incluse nel suo
  accordo sul trattamento dei dati.
- Google LLC (Firebase): Google aderisce al Data Privacy Framework UE-USA; i termini di
  Firebase includono anche le clausole contrattuali tipo.

Questi fornitori si avvalgono a loro volta di sub-responsabili vincolati agli stessi
obblighi. Puoi chiederci una copia di queste garanzie.

## 7. I tuoi diritti

Puoi chiederci di accedere ai tuoi dati, rettificarli, cancellarli, limitarne il
trattamento, riceverne una copia e opporti al trattamento basato sul legittimo interesse
(artt. 15-21 GDPR). Se il trattamento si basa sul consenso, puoi revocarlo in qualsiasi
momento, senza effetti su quanto fatto prima.

Poiché non esistono account, ci serve il tuo ID iSIMILAR per trovare i tuoi dati in
RevenueCat (sezione 9). I report degli errori e gli identificativi Firebase non sono
associati a quell'ID, quindi non possiamo sapere quali sono tuoi (art. 11 GDPR); restano
comunque validi i tempi indicati sopra.

Ti risponderemo entro un mese. Puoi anche proporre reclamo al Garante per la protezione dei
dati personali (www.garanteprivacy.it) o all'autorità del paese UE in cui vivi o lavori.

## 8. Sul tuo telefono

Impostazioni > Reimposta App cancella l'indice visivo e i dati di analisi. Disinstallare
l'app cancella tutto ciò che l'app salva sul telefono. In nessun caso vengono eliminate le
tue foto.

## 9. Cancellare i tuoi dati e contattarci

Istruzioni passo per passo: https://isimilar.app/it/delete-data

In breve: apri Impostazioni nell'app, tieni premuto il numero di versione per copiare il tuo
ID iSIMILAR e invialo a [EMAIL] con oggetto "Cancella i miei dati". Cancellare i dati non
annulla l'abbonamento; vedi i Termini d'uso.

## 10. Età

Devi avere almeno 14 anni, o l'età minima prevista dalla legge del tuo paese se superiore,
per utilizzare iSIMILAR.

Non raccogliamo consapevolmente dati di persone al di sotto di questa età. Se pensi che sia
successo, scrivici e li cancelleremo.

## 11. Decisioni automatizzate

Non prendiamo decisioni che ti riguardano basate unicamente su un trattamento
automatizzato e non creiamo profili pubblicitari.

## 12. Modifiche a questa informativa

Se cambia il modo in cui l'app usa i dati, aggiorneremo questa pagina e la data in alto
prima che la modifica arrivi nell'app. Se la modifica è importante, te lo diremo anche
nell'app.

## 13. Contatti

[EMAIL]
```

**Frase alternativa, para cuando haya un interruptor en Ajustes (recomendado, apartado 7):**
sustituye "How to object" de 5.2 (solo para los tres campos con interés legítimo) y de 5.3 por:
EN "Turn off 'Share diagnostics and usage data' in the app's Settings." · ES "Desactiva 'Compartir
diagnóstico y datos de uso' en los Ajustes de la app." · IT "Disattiva 'Condividi dati diagnostici e di
utilizzo' nelle Impostazioni dell'app."

---

## 2. Términos de uso

Cambios respecto a la v2: proveedor identificado con los marcadores nuevos; sin marcas de revisión; sin la
frase propuesta sobre autorización de padres (pasa al anexo A); plazo de 24 h redactado como consejo
válido para las dos tiendas; rutas de cancelación sin nombres de menú no verificados de Google Play.

### 2.1 Terms of Use (EN)

```
# iSIMILAR Terms of Use

Last updated: [FECHA]

## 1. Who we are and what these terms cover

iSIMILAR is provided and sold by [NOMBRE], self-employed, [DIRECCIÓN], VAT number
(P. IVA) [P. IVA], [REA si aplica], email [EMAIL] ("we", "us").

These terms apply to the iSIMILAR app for iOS and Android. By using the app you accept
them. If you downloaded iSIMILAR from the App Store, Apple's Standard Licensed
Application End User License Agreement
(https://www.apple.com/legal/internet-services/itunes/dev/stdeula/) also applies.

How we handle data is explained in the Privacy Policy: https://isimilar.app/privacy

## 2. Age

You must be at least 14 years old, or the minimum age required by the laws of your
country if higher, to use iSIMILAR.

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
  the current period.
- Payment is charged to your Apple ID or Google account by Apple or Google. We never see
  or store your payment details.

How to cancel:
- iPhone or iPad: Settings > [your name] > Subscriptions > iSIMILAR > Cancel
  Subscription, or https://apps.apple.com/account/subscriptions
- Android: open your subscriptions in Google Play, select iSIMILAR and tap Cancel
  subscription, or go to https://play.google.com/store/account/subscriptions
- In both cases, the "Manage Subscription" button in the app's Settings takes you there.

Uninstalling the app does not cancel the subscription. After you cancel, you keep PRO
until the end of the current period.

Restore Purchases: if you change phones or reinstall the app, tap "Restore Purchases" in
the app, signed in with the same Apple ID or Google account.

## 6. Refunds

Purchases are processed by Apple or Google, and refund requests are handled by them under
their own terms. This does not affect your rights as a consumer under the law.

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
country.

## 14. Contact

[EMAIL]
```

### 2.2 Términos de uso (ES)

```
# Términos de uso de iSIMILAR

Última actualización: [FECHA]

## 1. Quiénes somos y qué cubren estos términos

iSIMILAR la ofrece y la vende [NOMBRE], trabajador autónomo, [DIRECCIÓN], P. IVA [P. IVA],
[REA si aplica], correo [EMAIL] ("nosotros").

Estos términos se aplican a la app iSIMILAR para iOS y Android. Al usar la app los
aceptas. Si descargaste iSIMILAR desde la App Store, también se aplica el Contrato de
licencia de usuario final estándar de Apple
(https://www.apple.com/legal/internet-services/itunes/dev/stdeula/).

Cómo tratamos los datos se explica en la Política de privacidad:
https://isimilar.app/es/privacy

## 2. Edad

Debes tener al menos 14 años, o la edad mínima que exija la ley de tu país si es mayor,
para usar iSIMILAR.

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
  o del periodo en curso.
- El cobro lo hace Apple o Google en tu Apple ID o tu cuenta de Google. Nunca vemos ni
  guardamos tus datos de pago.

Cómo cancelar:
- iPhone o iPad: Ajustes > [tu nombre] > Suscripciones > iSIMILAR > Cancelar suscripción,
  o https://apps.apple.com/account/subscriptions
- Android: abre tus suscripciones en Google Play, elige iSIMILAR y toca Cancelar
  suscripción, o entra en https://play.google.com/store/account/subscriptions
- En los dos casos, el botón "Gestionar suscripción" de los Ajustes de la app te lleva
  allí.

Desinstalar la app no cancela la suscripción. Después de cancelar, mantienes PRO hasta el
final del periodo en curso.

Restaurar compras: si cambias de teléfono o reinstalas la app, toca "Restaurar compras" en
la app con el mismo Apple ID o la misma cuenta de Google.

## 6. Reembolsos

Las compras las procesa Apple o Google, y las solicitudes de reembolso las gestionan ellos
según sus propios términos. Esto no afecta a tus derechos como consumidor según la ley.

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
país.

## 14. Contacto

[EMAIL]
```

### 2.3 Termini d'uso (IT)

```
# Termini d'uso di iSIMILAR

Ultimo aggiornamento: [FECHA]

## 1. Chi siamo e cosa coprono questi termini

iSIMILAR è fornita e venduta da [NOMBRE], lavoratore autonomo, [DIRECCIÓN], P. IVA
[P. IVA], [REA si aplica], email [EMAIL] ("noi").

Questi termini si applicano all'app iSIMILAR per iOS e Android. Usando l'app li accetti.
Se hai scaricato iSIMILAR dall'App Store, si applica anche il Contratto di licenza
standard per l'utente finale di Apple
(https://www.apple.com/legal/internet-services/itunes/dev/stdeula/).

Il trattamento dei dati è spiegato nell'Informativa sulla privacy:
https://isimilar.app/it/privacy

## 2. Età

Devi avere almeno 14 anni, o l'età minima prevista dalla legge del tuo paese se superiore,
per utilizzare iSIMILAR.

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
  periodo in corso.
- L'addebito è effettuato da Apple o Google sul tuo ID Apple o account Google. Non vediamo
  né conserviamo mai i tuoi dati di pagamento.

Come annullare:
- iPhone o iPad: Impostazioni > [il tuo nome] > Abbonamenti > iSIMILAR > Annulla
  abbonamento, oppure https://apps.apple.com/account/subscriptions
- Android: apri i tuoi abbonamenti in Google Play, scegli iSIMILAR e tocca Annulla
  abbonamento, oppure vai su https://play.google.com/store/account/subscriptions
- In entrambi i casi, il pulsante "Gestisci abbonamento" nelle Impostazioni dell'app ti
  porta lì.

Disinstallare l'app non annulla l'abbonamento. Dopo l'annullamento, mantieni PRO fino alla
fine del periodo in corso.

Ripristina acquisti: se cambi telefono o reinstalli l'app, tocca "Ripristina acquisti"
nell'app con lo stesso ID Apple o account Google.

## 6. Rimborsi

Gli acquisti sono gestiti da Apple o Google, e le richieste di rimborso sono trattate da
loro secondo i rispettivi termini. Questo non pregiudica i tuoi diritti di consumatore
previsti dalla legge.

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
quel paese.

## 14. Contatti

[EMAIL]
```

**Nota sobre el plazo de 24 h.** Apple lo publica para la prueba: *"cancel it at least 24 hours before
the trial ends"* (support.apple.com/en-us/118428), y la App Store intenta renovar en las 24 h anteriores
al vencimiento (StoreKit, "Handling Subscriptions Billing"). Google Play no publica ningún plazo
(support.google.com/googleplay/answer/7018481 y la política de suscripciones, answer/9900533). La frase
está escrita como consejo ("para que no se te cobre, cancela al menos 24 horas antes"), que vale en las
dos tiendas porque cancelar antes nunca perjudica, y no atribuye la regla a Google.

---

## 3. Página de borrado de datos

Sin cambios de fondo respecto a la v2. Ajustes: marcadores nuevos, sin [VERIFICAR] en el texto
publicable y con el borrado del token de notificaciones.

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
- Turn off the weekly reminder in Settings: the app deletes its notification token.
- Delete everything: uninstall iSIMILAR. This deletes all the data the app stores on your
  phone. Your photos are not deleted.

## 2. Data held by our providers

1. Copy your iSIMILAR ID: open iSIMILAR > Settings, then press and hold the version number
   at the bottom of the screen. You will see "ID copied".
2. Email [EMAIL] with the subject "Delete my data" and paste your ID.
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

Deleting your data does not cancel your subscription. To cancel, use the "Manage
Subscription" button in the app's Settings, or go to
https://apps.apple.com/account/subscriptions (iPhone or iPad) or
https://play.google.com/store/account/subscriptions (Android).

If you use "Restore Purchases" after we delete your data, a new record is created so
that you keep PRO.

## 5. Questions

[EMAIL] · More details in the Privacy Policy: https://isimilar.app/privacy
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
- Desactiva el recordatorio semanal en Ajustes: la app borra su token de notificaciones.
- Borrarlo todo: desinstala iSIMILAR. Se borran todos los datos que la app guarda en tu
  teléfono. Tus fotos no se borran.

## 2. Datos que guardan nuestros proveedores

1. Copia tu ID de iSIMILAR: abre iSIMILAR > Ajustes y mantén pulsado el número de versión,
   al final de la pantalla. Verás el aviso "ID copied".
2. Escribe a [EMAIL] con el asunto "Borrar mis datos" y pega tu ID.
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

Borrar tus datos no cancela la suscripción. Para cancelarla, usa el botón "Gestionar
suscripción" de los Ajustes de la app, o entra en
https://apps.apple.com/account/subscriptions (iPhone o iPad) o
https://play.google.com/store/account/subscriptions (Android).

Si usas "Restaurar compras" después de que borremos tus datos, se crea un registro nuevo
para que mantengas PRO.

## 5. Dudas

[EMAIL] · Más detalles en la Política de privacidad: https://isimilar.app/es/privacy
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
- Disattiva il promemoria settimanale nelle Impostazioni: l'app cancella il suo token per
  le notifiche.
- Cancellare tutto: disinstalla iSIMILAR. Vengono cancellati tutti i dati che l'app salva
  sul telefono. Le tue foto non vengono eliminate.

## 2. Dati conservati dai nostri fornitori

1. Copia il tuo ID iSIMILAR: apri iSIMILAR > Impostazioni e tieni premuto il numero di
   versione in fondo alla schermata. Vedrai il messaggio "ID copied".
2. Scrivi a [EMAIL] con oggetto "Cancella i miei dati" e incolla il tuo ID.
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

Cancellare i dati non annulla l'abbonamento. Per annullarlo, usa il pulsante "Gestisci
abbonamento" nelle Impostazioni dell'app, oppure vai su
https://apps.apple.com/account/subscriptions (iPhone o iPad) o
https://play.google.com/store/account/subscriptions (Android).

Se usi "Ripristina acquisti" dopo che abbiamo cancellato i tuoi dati, viene creato un nuovo
record per mantenere PRO.

## 5. Domande

[EMAIL] · Maggiori dettagli nell'Informativa sulla privacy: https://isimilar.app/it/privacy
```

Comprobaciones operativas, fuera del texto publicable:
- Comprobar en el panel de RevenueCat si se puede buscar un cliente por número de pedido. Si no se
  puede, quitar el párrafo "Si ya no puedes abrir la app…".
- El plazo de 3 años obliga a borrar a mano o por API, al menos una vez al año, a los clientes sin
  actividad. RevenueCat no lo hace solo: su DPA conserva los datos mientras dure el contrato.
- El botón "Gestionar suscripción" solo aparece con PRO activo (`credits_hero.dart:19`, `isPremiumSync`),
  incluida la prueba. Es correcto, porque solo cancela quien está suscrito.

---

## 4. Etiqueta de App Store y formulario de Google Play

### 4.1 App Store Connect > App Privacy

Aplica la decisión de `definicion-tecnica.md:78`: identificadores y compras, vinculados; sin rastreo; sin
"Datos de rendimiento". "¿Recogéis datos?": **Sí**. "¿Se usan para rastrear?": **No** en todos.

| Tipo de dato | Qué es | SDK | Vinculado | Rastreo | Finalidades |
|---|---|---|---|---|---|
| Purchases > Purchase History | Compras, prueba y renovaciones | RevenueCat | **Sí** (decisión) | No | App Functionality, Analytics |
| Identifiers > User ID | ID aleatorio de RevenueCat | RevenueCat | **Sí** (decisión) | No | App Functionality, Analytics |
| Identifiers > Device ID | ID de instalación de Firebase (Remote Config, Crashlytics) y token de Cloud Messaging si se activa el recordatorio | Firebase | **Sí** (decisión) | No | App Functionality |
| Usage Data > Product Interaction | `paywall_trigger`, `batch_size` | RevenueCat | **Sí** (recomendado) | No | Analytics |
| Usage Data > Other Usage Data | `gallery_size`, `use_case` | RevenueCat | **Sí** (recomendado) | No | Analytics |
| Diagnostics > Crash Data | Informes de errores | Crashlytics | **Sí** (recomendado) | No | App Functionality |
| Diagnostics > Other Diagnostic Data | Modelo, versión del sistema y estado de la app al fallar | Crashlytics | **Sí** (recomendado) | No | App Functionality |

- **Performance Data:** se quita, según la decisión.
- **Lo que falta confirmar (no es contradicción, es un hueco):** la decisión cubre identificadores y
  compras, pero no dice nada de los datos de uso y diagnóstico.
  - Datos de uso: los atributos viajan con el mismo ID de usuario de RevenueCat, así que declararlos
    "no vinculados" sería incoherente.
  - Diagnóstico: los informes de Crashlytics van con un identificador de instalación. Por la regla de
    Apple, los datos personales cuentan como vinculados.
  - Recomiendo "vinculados" en los dos. **Confírmalo, Anibal.**
- **Sin "Developer's Advertising or Marketing":** las notificaciones no son promocionales.
- **Comprobar** que en el panel de RevenueCat no hay integraciones con terceros. Si las hubiera, cambiaría
  "rastreo" y "compartido".

### 4.2 Play Console > Contenido de la app > Seguridad de los datos

**Preguntas generales:** ¿se recogen datos?: **Sí**. ¿Cifrado en tránsito?: **Sí** (Firebase usa HTTPS;
RevenueCat cifra en tránsito). ¿Forma de pedir el borrado?: **Sí**, con https://isimilar.app/delete-data.
¿Se comparten?: **No** en todos los tipos, porque RevenueCat y Google son proveedores de servicios.

| Categoría > tipo | Qué es | SDK | Recogido | Compartido | Efímero | Obligatorio u opcional | Finalidades |
|---|---|---|---|---|---|---|---|
| Información financiera > Historial de compras | Compras | RevenueCat | Sí | No | No | Obligatorio | Funcionalidad de la app, Análisis |
| Actividad en la app > Interacciones con la app | `paywall_trigger`, `batch_size`, `gallery_size` | RevenueCat | Sí | No | No | Obligatorio | Análisis |
| Actividad en la app > Otras acciones | `use_case` | RevenueCat | Sí | No | No | **Opcional** | Análisis |
| Información y rendimiento de la app > Registros de fallos | Informes de errores | Crashlytics | Sí | No | No | Obligatorio | Funcionalidad de la app, Análisis |
| Información y rendimiento de la app > Diagnóstico | Modelo, versión del sistema, estado al fallar | Crashlytics | Sí | No | No | Obligatorio | Funcionalidad de la app, Análisis |
| Dispositivo u otros IDs | ID de instalación de Firebase (Remote Config, Crashlytics), token de Cloud Messaging e ID de usuario de RevenueCat | Firebase, RevenueCat | Sí | No | No | Obligatorio (el token es opcional, pero el tipo de dato en conjunto no lo es) | Funcionalidad de la app, Análisis, Comunicaciones del desarrollador |

- **Cloud Messaging:** entra por "Dispositivo u otros IDs" con "Comunicaciones del desarrollador" (Google:
  *"Used to send news or notifications about the app or the developer"*). Sin "Publicidad o marketing".
- **Remote Config:** entra por "Dispositivo u otros IDs". País, idioma, zona horaria y versión del sistema
  no son tipos de datos del formulario. Remote Config usa el *"device's country code"*, que interpreto
  como el de los ajustes, no la ubicación; por eso no se declara ubicación.
- **No se declaran:** fotos y vídeos (no salen del teléfono), ubicación ni información personal.
- **Coherencia con Apple:** mismos tipos, sin rastreo ni publicidad. Google no pregunta si los datos van
  "vinculados".

---

## 5. Muro de pago: `faq_a5` (cancelación)

**Texto actual** (`intl_*.arb`), con dos problemas:
- EN: "You can cancel anytime with one tap in your store settings. You keep PRO access until the end of the year."
- ES: "…Mantendrás el acceso PRO hasta fin de año." · IT: "…fino alla fine dell'anno."

1. "Until the end of the year" es falso para quien cancela durante la prueba y confuso en general: el
   periodo es de 12 meses desde la compra, no el año natural.
2. No dice nada de la prueba ni de cuándo cancelar para que no se cobre. Google exige explicar *"how and
   when a free trial will convert to a paid subscription"* (answer/9900533).

**La propuesta vale, con tres ajustes:**
1. Nombrar el botón con su texto real: "Manage Subscription", "Gestionar suscripción", "Gestisci
   abbonamento" (`manage_subscription`).
2. Cambiar "the period you've paid for" por "the current period". Quien cancela en la prueba no ha pagado
   nada.
3. La frase de las 24 h vale para las dos tiendas tal como está, porque es un consejo y no atribuye la
   regla a Google. Apple la publica para la prueba; Google no publica plazo, pero cancelar antes nunca
   perjudica.

**Texto final**

| Idioma | `faq_a5` |
|---|---|
| EN | Cancel anytime in your App Store or Google Play subscriptions; the "Manage Subscription" button in Settings takes you there. You keep PRO until the end of the current period. To avoid being charged after the free trial, cancel at least 24 hours before it ends. |
| ES | Cancela cuando quieras en tus suscripciones de App Store o Google Play; el botón "Gestionar suscripción" de Ajustes te lleva allí. Mantienes PRO hasta el final del periodo en curso. Para que no se te cobre al terminar la prueba gratuita, cancela al menos 24 horas antes de que acabe. |
| IT | Puoi annullare quando vuoi negli abbonamenti dell'App Store o di Google Play; il pulsante "Gestisci abbonamento" nelle Impostazioni ti porta lì. Mantieni PRO fino alla fine del periodo in corso. Per evitare l'addebito dopo la prova gratuita, annulla almeno 24 ore prima che finisca. |

Comprobar en pantalla que "Ajustes" / "Impostazioni" coincide con el título real de la pantalla de ajustes
en cada idioma.

**Fuera de lo pedido (se reporta, no se toca):** en el mismo muro, `faq_a3` dice "Very. … A circuit board
is a circuit board from any angle", y la precisión documentada es de en torno al 80%, mejor con el mismo
ángulo (`definicion-tecnica.md` · "Límites conocidos"). Es una promesa engañosa justo antes de cobrar.

---

## 6. Contradicciones detectadas

⚠️ Contradicción detectada (C1, sigue abierta desde la v2)
- Documento: `docs/definicion-tecnica.md` · "Arquitectura" (línea 22) y "Medición" (línea 111) dice: Firebase Analytics está fuera de la app; la próxima versión se publica sin la dependencia `firebase_analytics`.
- Fuente: `solopila/pubspec.yaml · línea 51` (`firebase_analytics: ^12.6.0`) y `lib/main.dart · línea 22` (`await AnalyticsService.init();`), comprobado hoy.
- Impacto: con el SDK dentro se envían eventos que la política v3 no declara. La política sería falsa y la etiqueta y el formulario, inexactos.
- Opciones: A) ajustar la fuente al documento (quitar la dependencia, el import y `init()`, y vaciar `_log()`) · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada (C5, nueva)
- Documento: `docs/definicion-tecnica.md` · "Datos y privacidad" (línea 70) dice: el token de Cloud Messaging se crea "solo cuando el usuario activa el recordatorio"; línea 80: por eso "la app no necesita pedir autorización".
- Fuente: `solopila/lib/views/image_selection_view.dart · línea 53` llama a `NotificationService.initFCM()` en `initState`, al abrir la pantalla principal, sin comprobar el recordatorio. `notification_service.dart · línea 145` pide ahí el permiso de notificaciones. No hay `FirebaseMessagingAutoInitEnabled` en iOS ni `firebase_messaging_auto_init_enabled` en Android, así que el SDK crea el token al arrancar. `setEnabled(false)` (`notification_service.dart:62-64`) solo cancela el recordatorio local y no borra el token.
- Impacto: alto. La política v3 (sección 5.4) y la conclusión de consentimiento del documento dependen de este punto. Con el código actual, el token se crea sin consentimiento y la política es falsa.
- Opciones: A) ajustar la fuente al documento (desactivar la creación automática en `Info.plist` y `AndroidManifest.xml`; llamar a `initFCM()` y activar la creación automática solo dentro de `setEnabled(true)`, después de aceptar el permiso; llamar a `deleteToken()` en `setEnabled(false)`) · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada (C3, sigue abierta)
- Documento: `docs/definicion-tecnica.md` · "Modelo comercial en el código" (línea 56) dice: 11,99 USD en EE. UU.
- Fuente: `solopila/lib/services/premium_service.dart · líneas 84-85 y 90-91` dice: `'$12.99'` como precio de respaldo.
- Impacto: el muro de pago puede mostrar un precio distinto del que se cobra y del que dicen los términos.
- Opciones: A) ajustar la fuente al documento (sin precio fijo; botón desactivado si la tienda no responde) · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada (C2, solo queda la parte de la guía)
- Documento: `docs/definicion-tecnica.md` · línea 78 dice: identificadores y compras se declaran **vinculados**.
- Fuente: `docs/guia-estrategica.md` · "Prioridades" (línea 202) dice: hay que publicar en la web que la etiqueta declara datos "no vinculados a la persona y sin publicidad".
- Impacto: si la web sigue la guía, contradirá la etiqueta nueva. Riesgo bajo mientras nadie redacte la página a partir de esa línea.
- Opciones: A) ajustar la fuente al documento (que la guía diga "sin rastreo y sin publicidad") · B) Anibal revisa el documento
- Esperando decisión.

C4 de la v2 queda resuelta: el documento ya dice que Crashlytics solo recoge informes de errores y que se
quita "Datos de rendimiento".

---

## 7. Riesgos de publicar sin abogado

Ordenados de mayor a menor. **Ninguno, por sí solo, impide publicar**, siempre que se cumplan las
condiciones del apartado 0. Lo que sí impide publicar es que el código no coincida con la política (C1 y
C5): eso no lo arregla un abogado, sino la sesión en `solopila/`.

1. **Medio: la forma de oponerse es débil.** Para Crashlytics y para los tres atributos con interés
   legítimo, el único mecanismo es escribir un correo. En Crashlytics ni siquiera podemos localizar los
   informes del usuario, y en RevenueCat los atributos pueden volver a generarse. El art. 21 del RGPD
   exige que la oposición sea efectiva. La corrección barata es un interruptor en Ajustes ("Compartir
   diagnóstico y datos de uso") que llame a `setCrashlyticsCollectionEnabled(false)` y deje de enviar
   esos tres atributos. La frase para la política ya está preparada al final del apartado 1. **Es lo que
   más recomiendo hacer antes o poco después de publicar.**
2. **Medio-bajo: ePrivacy (art. 122 del Codice privacy) sin consentimiento.** La decisión aplica interés
   legítimo a Crashlytics y a los atributos de RevenueCat, y deja la creación del token supeditada al
   consentimiento. Es una postura defendible: no hay publicidad ni perfiles, el volumen de datos es mínimo
   y las directrices del Garante de 2021 admiten la medición agregada sin consentimiento con condiciones.
   Pero no es seguro: `gallery_size` sale de información guardada en el teléfono, y el CEPD interpreta el
   art. 5.3 de forma amplia. Con el interruptor del punto 1, el riesgo baja.
3. **Bajo: datos de identificación en la web.** Si falta la P. IVA en la página de inicio (DPR 633/1972,
   art. 35) o los datos del D.Lgs. 70/2003, art. 7, se expone a sanciones administrativas. Se resuelve
   rellenando los marcadores y añadiendo un pie en todas las páginas.
4. **Bajo: cláusulas de consumo.** Los términos v3 están redactados a favor del consumidor: no excluyen
   la garantía, no imponen fuero ni tope de responsabilidad. El riesgo de nulidad es menor que con los
   términos antiguos.
5. **Bajo: registro de actividades (art. 30 del RGPD).** Probablemente es obligatorio, porque el
   tratamiento es continuo. Se puede hacer sin abogado con la plantilla del Garante: una tabla con los
   cinco servicios de la sección 5.

---

## Anexo A · Revisión futura recomendada (antes en la lista [ABOGADO])

Para cuando haya presupuesto. Ninguno de estos puntos aparece ya marcado en el texto publicable.

| # | Tema | Pregunta |
|---|---|---|
| 1 | ePrivacy y bases jurídicas | ¿Bastan el interés legítimo para Crashlytics y los atributos de RevenueCat, y el consentimiento solo para el token? Documentar la ponderación del interés legítimo (art. 5.2 del RGPD). |
| 2 | Mecanismo de oposición | ¿Basta el correo, o hace falta el interruptor en la app? |
| 3 | Transferencias | ¿Están aceptados el DPA de RevenueCat (cláusulas contractuales tipo, módulo 2) y los Data Processing and Security Terms de Firebase, con el contacto de privacidad rellenado? ¿Hace falta una evaluación de impacto de la transferencia para RevenueCat? |
| 4 | Plazos | ¿Son adecuados 3 años para RevenueCat y 24 meses para los correos? Los registros contables, 10 años según el art. 2220 del Codice civile, son los informes de venta de las tiendas, no los datos por usuario. |
| 5 | Identificación | ¿Domicilio profesional o de residencia en la web? ¿Hay inscripción en el REA? ¿Coinciden los datos de comerciante de la UE en la App Store? |
| 6 | Menores | 14 años para el consentimiento (Codice privacy, art. 2-quinquies) frente a la capacidad para contratar una suscripción: ¿añadir una frase sobre la autorización de los padres para compras de menores de 18? |
| 7 | Desistimiento y reembolsos | Codice del Consumo, art. 59, letra o, y el papel de Apple y Google como vendedores o comisionistas. |
| 8 | Responsabilidad, garantía de conformidad del contenido digital (Codice del Consumo, arts. 135-octies y ss.), ley aplicable (Roma I, art. 6) y fuero del consumidor | Revisar los apartados 11 y 13 de los términos. |
| 9 | EULA | ¿Mantener el EULA estándar de Apple con estos términos como complemento? |
| 10 | Registro del art. 30 | Confirmar que es obligatorio y validar la tabla. |
| 11 | Idioma que prevalece | ¿Añadir qué versión prevalece en caso de discrepancia? |
| 12 | Web isimilar.app | Si usa analítica o cookies no técnicas, necesita su propio aviso. |
| 13 | Plataforma ODR | Creo que la plataforma europea de resolución de litigios en línea cerró en julio de 2025: no enlazarla sin comprobarlo. |

---

## Fuentes (consultadas el 22-10-2026)

Las mismas que en la v2, apartado 8. Además:
- Firebase, gestión de tokens de Cloud Messaging (270 días en Android): https://firebase.google.com/docs/cloud-messaging/manage-tokens
- Firebase, privacidad (Crashlytics 90 días; IDs de instalación, 180 días tras borrarse): https://firebase.google.com/support/privacy
- Apple Support, cancelar una prueba al menos 24 h antes: https://support.apple.com/en-us/118428
- Google Play, política de suscripciones (sin plazo de 24 h): https://support.google.com/googleplay/android-developer/answer/9900533
