# Política de privacidad, /delete-data/ y tiendas por T4b (interruptor "Compartir datos técnicos")

> **Decidido por hq (2026-10-31):** se aplica todo, incluido B.4. Crashlytics borra los informes
> pendientes (`deleteUnsentReports`), así que vale la frase entre corchetes de 5.3. Las
> contradicciones de G quedan resueltas en `docs/` (commit de hoy). Fecha compartida con
> Términos: se acepta.

**Estado: borrador. Publicar a la vez que la versión de la app con T4b, no antes.**

Autor: agente `legal-tiendas`, 2026-10-31. No soy abogado; los puntos que lo necesitan están marcados.
Fuentes leídas: `solopila_landingPAGE/astro/src/legal/{en,es,it}/privacy.md` y `delete-data.md`,
`astro/src/legal/datos.json`, `docs/definicion-tecnica.md` (Datos y privacidad, Consentimiento,
Medición), `docs/brief-marketing.md`, `borradores/2026-10-22-instrucciones-app.md` (T4b),
`solopila/lib/services/analytics_service.dart`, `solopila/lib/viewmodels/home_view_model.dart`,
`solopila/pubspec.yaml`. Web publicada comprobada el 2026-10-31 (`isimilar.app/privacy/`: "Last
updated: October 23, 2026").

Estado del código: T4b **no está programado todavía** (en `solopila/lib` no hay
`setCrashlyticsCollectionEnabled` ni el interruptor). Este borrador describe el comportamiento
decidido, no el comprobado. Antes de publicar hay que verificarlo en la app (sección F).

---

## A. Condiciones previas: lo que la app tiene que hacer para que estos textos sean ciertos

Las añado aquí porque los textos dependen de ellas. No las decido: las decide Anibal.

1. **Crashlytics guarda en el teléfono los errores ocurridos con la recogida desactivada y los
   envía si se vuelve a activar.** Documentación de Firebase para Flutter ("Enable opt-in
   reporting"): con la recogida desactivada, *"Crashlytics will store crash information locally on
   the device"*; al activarla, *"any crash information stored on the device will be sent"*.
   Recomendación para T4b: con el interruptor apagado, llamar a
   `FirebaseCrashlytics.instance.deleteUnsentReports()` (al apagarlo y en cada arranque). Si no se
   hace, quien vuelve a activar el interruptor envía errores de cuando lo tenía apagado.
   - Con `deleteUnsentReports`: usar las frases entre corchetes [ ] de 5.3.
   - Sin él: quitar la frase entre corchetes y añadir en su lugar: "Si lo vuelves a activar, la
     app puede enviar los errores guardados mientras estaba desactivado." (no recomendado).
2. **El cambio de Crashlytics se aplica en el siguiente arranque.** Firebase: *"apply the next
   time the user launches the app"* (Flutter) y *"The value does not apply until the next run of
   the app"* (referencia de iOS). Por eso el texto dice "a partir de la próxima vez que abras la
   app" y no "al momento". El ajuste persiste: *"The override value persists across all subsequent
   launches of your app"*.
3. **Borrado en RevenueCat.** RevenueCat: *"Any attribute can be cleared by passing null or an
   empty string"*. Los atributos se sincronizan al arrancar, al pasar a segundo plano y al comprar
   o restaurar, no al instante. La instrucción T4b ya pide "comprobar que el borrado llega también
   si se desactiva sin red". Si esa prueba falla, el texto "borra de RevenueCat los que ya había
   enviado" no es cierto y hay que corregir la app antes de publicar. No puedo confirmar si
   RevenueCat guarda un historial de valores anteriores: su documentación no lo dice.
4. **"Restablecer App" no debe volver a activar el interruptor.** No puedo confirmar qué hará
   (está pendiente T4e). Si Reset borra SharedPreferences pero el ajuste nativo de Crashlytics
   sigue apagado, el interruptor mostraría "activado" con Crashlytics apagado, o al revés.
   Recomiendo que Reset conserve la elección. Por esta duda **no toco el apartado 3** de la
   política ("Ajustes de la app... se borra con Restablecer App").
5. **Reinstalar.** Al desinstalar se borran los ajustes en iOS. En Android, la copia de seguridad
   automática puede restaurar SharedPreferences; no puedo confirmar qué pasa con el ajuste propio
   de Crashlytics. Por eso el texto dice "si reinstalas la app, revisa este ajuste" en vez de
   prometer un estado concreto.

---

## B. Política de privacidad: cambios por idioma

Resumen de apartados: **1** (resumen), **5.2**, **5.3** y **7** cambian. **2, 3, 4, 5.1, 5.4–5.7,
6, 8–13** no cambian. Apartado 12: no lo considero un "cambio importante" que obligue a avisar en
la app (añade una opción al usuario y no recoge datos nuevos); es una valoración, no una opinión
jurídica.

### B.1 Inglés (`legal/en/privacy.md`)

**Apartado 1, tercer punto**

ANTES:
```
- To sell and manage the subscription, fix errors, check for required updates and, if you
  turn them on, send notifications, the app sends technical data about purchases, usage
  and errors to the providers listed in section 5. This data never includes your photos or
  the content of your gallery.
```
DESPUÉS:
```
- To sell and manage the subscription, fix errors, check for required updates and, if you
  turn them on, send notifications, the app sends technical data about purchases, usage
  and errors to the providers listed in section 5. This data never includes your photos or
  the content of your gallery. You can turn off error reports and usage data in Settings
  with "Share technical data to improve the app" (sections 5.2 and 5.3); purchases keep
  working.
```

**Apartado 5.2, última línea ("How to object or withdraw consent")**

ANTES:
```
How to object or withdraw consent: email us with your iSIMILAR ID (section 9) and we will
delete these fields. The app may record new ones the next time the PRO screen opens; if
you ask, we will delete those too.
```
DESPUÉS:
```
How to object or withdraw consent: turn off "Share technical data to improve the app" in
the app's Settings. The app then stops sending these fields, deletes from RevenueCat the
ones it had already sent and no longer shows the question about what you use iSIMILAR
for. Purchases and Restore Purchases keep working. If you turn it back on, the app may
record these fields again. You can also email us with your iSIMILAR ID (section 9) and we
will delete these fields; to stop the app from recording new ones, turn off the option.
```

**Apartado 5.3, última línea ("How to object")**

ANTES:
```
How to object: email us. Because error reports are not linked to your iSIMILAR ID, we
cannot pick out yours; reports stop when you uninstall the app and are deleted after 90
days.
```
DESPUÉS:
```
How to object: turn off "Share technical data to improve the app" in the app's Settings.
From the next time you open the app, it stops sending error reports[, and errors that
happen while the option is off are never sent, even if you turn it back on later]. If you
reinstall the app, check this option again. Reports already sent are not linked to your
iSIMILAR ID, so we cannot pick out yours; they are deleted after 90 days. You can also
email us, but for the same reason we cannot stop your reports ourselves.
```

**Apartado 7, segundo párrafo**

ANTES:
```
Because there is no account, we need your iSIMILAR ID to find your data in RevenueCat
(section 9). Error reports and Firebase identifiers are not linked to that ID, so we
cannot identify which ones are yours (Art. 11 GDPR); the retention periods above still
apply.
```
DESPUÉS:
```
Because there is no account, we need your iSIMILAR ID to find your data in RevenueCat
(section 9). Error reports and Firebase identifiers are not linked to that ID, so we
cannot identify which ones are yours (Art. 11 GDPR); the retention periods above still
apply. To stop error reports, use the option described in section 5.3.
```

### B.2 Español (`legal/es/privacy.md`)

**Apartado 1, tercer punto**

ANTES:
```
- Para vender y gestionar la suscripción, corregir errores, comprobar si hace falta
  actualizar y, si las activas, enviarte notificaciones, la app envía datos técnicos de
  compras, uso y errores a los proveedores del apartado 5. Esos datos nunca incluyen tus
  fotos ni el contenido de tu galería.
```
DESPUÉS:
```
- Para vender y gestionar la suscripción, corregir errores, comprobar si hace falta
  actualizar y, si las activas, enviarte notificaciones, la app envía datos técnicos de
  compras, uso y errores a los proveedores del apartado 5. Esos datos nunca incluyen tus
  fotos ni el contenido de tu galería. Puedes desactivar los informes de errores y los
  datos de uso en Ajustes, con "Compartir datos técnicos para mejorar la app" (apartados
  5.2 y 5.3); las compras siguen funcionando.
```

**Apartado 5.2, última línea**

ANTES:
```
Cómo oponerte o retirar el consentimiento: escríbenos con tu ID de iSIMILAR (apartado 9) y
borraremos estos campos. La app puede registrar campos nuevos la próxima vez que se abra
la pantalla de PRO; si nos lo pides, también los borraremos.
```
DESPUÉS:
```
Cómo oponerte o retirar el consentimiento: desactiva "Compartir datos técnicos para mejorar
la app" en los Ajustes de la app. La app deja de enviar estos campos, borra de RevenueCat
los que ya había enviado y deja de mostrar la pregunta sobre para qué usas iSIMILAR. Las
compras y "Restaurar compras" siguen funcionando. Si vuelves a activarlo, la app puede
registrar estos campos de nuevo. También puedes escribirnos con tu ID de iSIMILAR
(apartado 9) y borraremos estos campos; para que la app no registre otros nuevos,
desactiva el ajuste.
```

**Apartado 5.3, última línea**

ANTES:
```
Cómo oponerte: escríbenos. Como los informes no están asociados a tu ID de iSIMILAR, no
podemos distinguir los tuyos; dejan de enviarse al desinstalar la app y se borran a los 90
días.
```
DESPUÉS:
```
Cómo oponerte: desactiva "Compartir datos técnicos para mejorar la app" en los Ajustes de
la app. A partir de la próxima vez que abras la app, deja de enviar informes de errores[, y
los errores que ocurran mientras esté desactivado no se envían nunca, aunque después lo
vuelvas a activar]. Si reinstalas la app, revisa de nuevo este ajuste. Los informes ya
enviados no están asociados a tu ID de iSIMILAR, así que no podemos distinguir los tuyos;
se borran a los 90 días. También puedes escribirnos, pero por ese mismo motivo no podemos
detener tus informes por nuestra cuenta.
```

**Apartado 7, segundo párrafo**

ANTES:
```
Como no hay cuentas, necesitamos tu ID de iSIMILAR para encontrar tus datos en RevenueCat
(apartado 9). Los informes de errores y los identificadores de Firebase no están asociados
a ese ID, así que no podemos saber cuáles son tuyos (art. 11 RGPD); aun así se les aplican
los plazos indicados arriba.
```
DESPUÉS:
```
Como no hay cuentas, necesitamos tu ID de iSIMILAR para encontrar tus datos en RevenueCat
(apartado 9). Los informes de errores y los identificadores de Firebase no están asociados
a ese ID, así que no podemos saber cuáles son tuyos (art. 11 RGPD); aun así se les aplican
los plazos indicados arriba. Para dejar de enviar informes de errores, usa el ajuste del
apartado 5.3.
```

### B.3 Italiano (`legal/it/privacy.md`)

**Sezione 1, terzo punto**

ANTES:
```
- Per vendere e gestire l'abbonamento, correggere gli errori, verificare se serve un
  aggiornamento e, se le attivi, inviarti notifiche, l'app invia dati tecnici su acquisti,
  utilizzo ed errori ai fornitori elencati nella sezione 5. Questi dati non includono mai
  le tue foto né il contenuto della galleria.
```
DESPUÉS:
```
- Per vendere e gestire l'abbonamento, correggere gli errori, verificare se serve un
  aggiornamento e, se le attivi, inviarti notifiche, l'app invia dati tecnici su acquisti,
  utilizzo ed errori ai fornitori elencati nella sezione 5. Questi dati non includono mai
  le tue foto né il contenuto della galleria. Puoi disattivare i report degli errori e i
  dati di utilizzo nelle Impostazioni, con "Condividi dati tecnici per migliorare l'app"
  (sezioni 5.2 e 5.3); gli acquisti continuano a funzionare.
```

**Sezione 5.2, ultima riga**

ANTES:
```
Come opporti o revocare il consenso: scrivici con il tuo ID iSIMILAR (sezione 9) e
cancelleremo questi campi. L'app potrebbe registrarne di nuovi la prossima volta che si
apre la schermata PRO; se ce lo chiedi, cancelleremo anche quelli.
```
DESPUÉS:
```
Come opporti o revocare il consenso: disattiva "Condividi dati tecnici per migliorare
l'app" nelle Impostazioni dell'app. L'app smette di inviare questi campi, cancella da
RevenueCat quelli già inviati e non mostra più la domanda su per cosa usi iSIMILAR. Gli
acquisti e "Ripristina acquisti" continuano a funzionare. Se la riattivi, l'app potrebbe
registrare di nuovo questi campi. Puoi anche scriverci con il tuo ID iSIMILAR (sezione 9)
e cancelleremo questi campi; per evitare che l'app ne registri di nuovi, disattiva
l'opzione.
```

**Sezione 5.3, ultima riga**

ANTES:
```
Come opporti: scrivici. Poiché i report non sono associati al tuo ID iSIMILAR, non possiamo
individuare i tuoi; smettono di essere inviati quando disinstalli l'app e vengono
cancellati dopo 90 giorni.
```
DESPUÉS:
```
Come opporti: disattiva "Condividi dati tecnici per migliorare l'app" nelle Impostazioni
dell'app. Dalla prossima volta che apri l'app, smette di inviare i report degli errori[, e
gli errori che si verificano mentre l'opzione è disattivata non vengono mai inviati, anche
se in seguito la riattivi]. Se reinstalli l'app, controlla di nuovo questa opzione. I
report già inviati non sono associati al tuo ID iSIMILAR, quindi non possiamo individuare i
tuoi; vengono cancellati dopo 90 giorni. Puoi anche scriverci, ma per lo stesso motivo non
possiamo interrompere i tuoi report al posto tuo.
```

**Sezione 7, secondo paragrafo**

ANTES:
```
Poiché non esistono account, ci serve il tuo ID iSIMILAR per trovare i tuoi dati in
RevenueCat (sezione 9). I report degli errori e gli identificativi Firebase non sono
associati a quell'ID, quindi non possiamo sapere quali sono tuoi (art. 11 GDPR); restano
comunque validi i tempi indicati sopra.
```
DESPUÉS:
```
Poiché non esistono account, ci serve il tuo ID iSIMILAR per trovare i tuoi dati in
RevenueCat (sezione 9). I report degli errori e gli identificativi Firebase non sono
associati a quell'ID, quindi non possiamo sapere quali sono tuoi (art. 11 GDPR); restano
comunque validi i tempi indicati sopra. Per smettere di inviare i report degli errori, usa
l'opzione descritta nella sezione 5.3.
```

### B.4 Cambio adicional, no es de T4b (decide Anibal): lista de `paywall_trigger` en 5.2

La política lista 4 orígenes del muro; el código y la definición técnica tienen 6 (T4h ya está en
`solopila`, commit 340dfdf, y saldrá en la misma versión). Ver contradicción 1 en la sección G.
Texto propuesto si se elige la opción A:

- EN ANTES: `(a camera search, a batch delete, a batch move to an album, or the button in Settings).`
  EN DESPUÉS: `(a camera search, a batch delete, a batch move to an album, the button in Settings, or the camera search counter or the PRO button on the main screen).`
- ES ANTES: `(una búsqueda con la cámara, un borrado en lote, mover en lote a un álbum o el botón de Ajustes).`
  ES DESPUÉS: `(una búsqueda con la cámara, un borrado en lote, mover en lote a un álbum, el botón de Ajustes, o el contador de búsquedas con cámara o el botón PRO de la pantalla principal).`
- IT ANTES: `(una ricerca con la fotocamera, un'eliminazione multipla, uno spostamento multiplo in un album o il pulsante nelle Impostazioni).`
  IT DESPUÉS: `(una ricerca con la fotocamera, un'eliminazione multipla, uno spostamento multiplo in un album, il pulsante nelle Impostazioni, oppure il contatore delle ricerche con la fotocamera o il pulsante PRO nella schermata principale).`

Si T4c (`batch_share`) entra en la misma versión, añadir también "a batch share / compartir en
lote / una condivisione multipla". No puedo confirmar si T4c entra en esta versión.

---

## C. Página `/delete-data/`: sí debe mencionar el interruptor

Es la URL de borrado declarada en Google Play y hoy dice que los informes de errores solo dejan de
enviarse al desinstalar. Dos cambios por idioma.

### C.1 Apartado 1: nuevo punto después del del recordatorio semanal

- EN (añadir tras "- Turn off the weekly reminder in Settings: the app deletes its notification token."):
```
- Turn off "Share technical data to improve the app" in Settings: the app stops sending
  error reports and measurement fields, and deletes from RevenueCat the measurement fields
  it had already sent. Your purchase information is kept, so you keep PRO.
```
- ES (añadir tras "- Desactiva el recordatorio semanal en Ajustes: la app borra su token de notificaciones."):
```
- Desactiva "Compartir datos técnicos para mejorar la app" en Ajustes: la app deja de
  enviar informes de errores y campos de medición, y borra de RevenueCat los campos de
  medición que ya había enviado. La información de tu compra se mantiene, así que
  conservas PRO.
```
- IT (aggiungere dopo "- Disattiva il promemoria settimanale nelle Impostazioni: l'app cancella il suo token per le notifiche."):
```
- Disattiva "Condividi dati tecnici per migliorare l'app" nelle Impostazioni: l'app smette
  di inviare i report degli errori e i campi di misurazione, e cancella da RevenueCat i
  campi di misurazione già inviati. Le informazioni sull'acquisto restano, quindi mantieni
  PRO.
```

Nota: el apartado 1 se titula "Datos en tu teléfono", pero ya incluye el recordatorio, que también
borra un dato de un proveedor. Lo pongo ahí por coherencia con ese punto.

### C.2 Apartado 3, primer punto: última frase

- EN ANTES: `Once you uninstall the app, it stops sending any data.`
  EN DESPUÉS: `Once you uninstall the app, it stops sending any data. To stop error reports without uninstalling, turn off "Share technical data to improve the app" in Settings.`
- ES ANTES: `Al desinstalar la app, deja de enviar cualquier dato.`
  ES DESPUÉS: `Al desinstalar la app, deja de enviar cualquier dato. Para dejar de enviar informes de errores sin desinstalarla, desactiva "Compartir datos técnicos para mejorar la app" en Ajustes.`
- IT ANTES: `Una volta disinstallata, l'app smette di inviare qualsiasi dato.`
  IT DESPUÉS: `Una volta disinstallata, l'app smette di inviare qualsiasi dato. Per smettere di inviare i report degli errori senza disinstallarla, disattiva "Condividi dati tecnici per migliorare l'app" nelle Impostazioni.`

---

## D. Fecha de "última actualización" y versión

- La política no tiene número de versión. La fecha sale de `astro/src/legal/datos.json`
  (`FECHA`: "October 23, 2026" / "23 de octubre de 2026" / "23 ottobre 2026").
- **Sí cambia:** poner la fecha del día en que se publique (la de salida de la versión con T4b).
- **Ojo:** `FECHA` es una sola variable para privacidad **y términos** (`Legal.astro:23`). Si se
  cambia, los Términos también mostrarán la fecha nueva aunque no cambien. Opciones: aceptarlo
  (inofensivo) o separar la fecha por documento en una sesión de la web. Decide Anibal.
- `/delete-data/` no muestra fecha.
- Momento: el apartado 12 promete actualizar la página "antes de que el cambio llegue a la app".
  Para cumplir eso y "no antes", recomiendo publicación manual de la versión en App Store
  ("Manually release this version") y publicación gestionada en Google Play, y subir la web justo
  antes de liberar la versión.

---

## E. Tiendas

### E.1 Google Play: formulario de seguridad de datos

Norma (support.google.com/googleplay/android-developer/answer/10787469): solo se puede declarar
opcional si todos los usuarios, en cualquier dispositivo o región, pueden aportar el dato, darse de
baja o darse de alta; *"'Optional' includes the ability to opt into or opt out of data
collection."* El formulario describe *"the sum of your app's data collection and sharing across all
its versions currently distributed on Google Play"*, y *"Your Data safety form responses must remain
accurate and complete at all times."*

No veo la consola: no puedo confirmar qué hay declarado hoy (la tarea del formulario sigue abierta en
`pendientes.md`). La tabla parte del formulario recomendado en `borradores/2026-10-22-legal-politicas-v3.md`, apartado 4.2.

| Tipo de dato | Origen | Hoy (recomendado v3) | Con T4b | Cambia |
|---|---|---|---|---|
| Información y rendimiento de la app > Registros de fallos | Crashlytics | Obligatorio | **Opcional** | Sí |
| Información y rendimiento de la app > Diagnóstico | Crashlytics (estado y datos del dispositivo al fallar) | Obligatorio | **Opcional** | Sí, si está declarado |
| Actividad en la app > Interacciones con la app | `paywall_trigger`, `batch_size`, `gallery_size` (RevenueCat) | Obligatorio | **Opcional** | Sí |
| Actividad en la app > Otras acciones | `use_case` | Opcional | Opcional | No |
| Información financiera > Historial de compras | RevenueCat | Obligatorio | Obligatorio | No |
| Dispositivo u otros IDs | ID de RevenueCat, ID de instalación de Firebase (Remote Config), token FCM | Obligatorio | Obligatorio | No (Remote Config y RevenueCat siguen) |

Sin cambios: "¿Recoge datos?" Sí; compartido: No; cifrado en tránsito: Sí; forma de pedir el
borrado: Sí (`https://isimilar.app/delete-data/`); finalidades; sin publicidad.

Comprobado en fuentes oficiales: RevenueCat declara que su SDK *"does not collect app activity"* ni
*"crash logs or diagnostics"*, así que "Interacciones con la app" viene solo de nuestros atributos y
puede pasar a opcional. Firebase (play-data-disclosure) no asigna sus datos a tipos de Google Play;
la asignación de "Diagnóstico" a Crashlytics es nuestra.

**Cuándo cambiarlo:** cuando la versión con T4b esté al 100 % en producción y no quede ninguna
versión sin el interruptor distribuida en otra pista. Durante un lanzamiento escalonado sigue
distribuyéndose la versión antigua, que no permite darse de baja; marcarlo opcional antes sería
inexacto. Llegar tarde es menos grave (declarar "obligatorio" algo opcional sobredeclara, no
engaña). No puedo confirmar cómo trata Google los lanzamientos escalonados en este punto; lo
prudente es esperar al 100 %.

### E.2 App Store: etiqueta de privacidad

**No cambia nada.** Apple no tiene campo de obligatorio u opcional. Las dos excepciones que
permitirían no declarar datos no se cumplen (developer.apple.com/app-store/app-privacy-details):
- "Optional disclosure": exige recogida infrecuente, iniciada por el usuario cada vez y con su
  nombre visible en el formulario; aquí la recogida es continua.
- "Product Improvement Programs": exige que el usuario *"explicitly opts in"* y que los datos no
  estén vinculados; aquí el interruptor viene activado y los datos van vinculados.
Siguen declarados igual: identificadores, compras, datos de uso y diagnóstico, vinculados y sin
rastreo. Opcional: en App Store Connect se puede poner `https://isimilar.app/delete-data/` como URL
de "Privacy Choices".

---

## F. Riesgos y comprobaciones antes de publicar

| Requisito | Estado | Evidencia | Acción |
|---|---|---|---|
| Enlace a la política dentro de la app (Apple 5.1.1(i)) | no cumple (en esta versión) | T4d pendiente: la app enlaza a Notion, que no describe T4b | T4d tiene que salir en la misma versión que T4b |
| La política explica cómo retirar el consentimiento (Apple 5.1.1(i)) | cumple con este borrador | apartados 5.2 y 5.3 nuevos | Publicar con la versión |
| "Secure user consent" para datos de uso (Apple 5.1.1(ii)) | sin verificar | El interruptor viene activado: es baja voluntaria, no consentimiento previo | Riesgo de rechazo bajo en la práctica; no puedo confirmar cómo lo aplica App Review. **Abogado:** la cuestión ePrivacy (art. 122 del Codice privacy) ya estaba abierta en la definición técnica |
| Interruptor apaga Crashlytics | sin verificar | No programado; Firebase lo aplica en el siguiente arranque | Probar: apagar, cerrar, provocar un error, comprobar que no llega a la consola |
| Errores guardados con el interruptor apagado no se envían al reactivar | sin verificar | Firebase guarda los informes en el teléfono | `deleteUnsentReports()` (sección A.1) |
| Borrado de atributos en RevenueCat | sin verificar | Instrucción T4b, opción B | Comprobar en la ficha del cliente de RevenueCat, con y sin red |
| Pregunta `use_case` oculta con el interruptor apagado | sin verificar | No programado | Probar tras una compra de prueba (sandbox) |
| Compras y "Restaurar compras" con el interruptor apagado | sin verificar | RevenueCat no se desactiva | Probar en sandbox |
| Reset App y reinstalación no cambian la elección por sorpresa | sin verificar | Sección A.4 y A.5 | Probar (va con T4e) |
| Terminología "seudónimos", nunca "anónimos" | cumple | Ningún texto nuevo dice "anónimos" | — |

---

## G. Contradicciones y huecos con `docs/`

⚠️ Contradicción detectada
- Documento: `docs/definicion-tecnica.md` · Medición, tabla de atributos (línea 100) dice:
  `paywall_trigger` toma `camera`, `batch_delete`, `batch_album`, `settings`, `home_counter`,
  `home_appbar`.
- Fuente: `solopila_landingPAGE/astro/src/legal/{en,es,it}/privacy.md` · 5.2 (líneas 87-88 EN)
  dice: solo búsqueda con cámara, borrado en lote, mover en lote y botón de Ajustes. El código
  (`analytics_service.dart:34-35`) ya tiene los dos valores nuevos.
- Impacto: con la próxima versión, la política describiría de forma incompleta lo que se envía
  (Apple 5.1.1(i) pide identificar todos los datos).
- Opciones: A) ajustar la fuente al documento (texto en B.4) · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada
- Documento: `docs/definicion-tecnica.md` · Pendiente de confirmar (línea 162) dice: "según la
  última revisión del código, `setAttributes` solo envía el motivo del muro, `gallery_size` y
  `use_case`".
- Fuente: `solopila/lib/services/analytics_service.dart:79` dice:
  `if (batchSize != null) attributes['batch_size'] = batchSize.toString();`
- Impacto: ninguno para la política (ya declara `batch_size`); el pendiente del documento está
  desfasado y se puede cerrar.
- Opciones: A) ajustar la fuente al documento (quitar `batch_size` del código y de la política) ·
  B) Anibal revisa el documento (cerrar el pendiente: sí se envía)
- Esperando decisión.

Hueco, no contradicción: `docs/definicion-tecnica.md` · Consentimiento (línea 84) dice que el
interruptor "desactiva Crashlytics, el envío de atributos de medición a RevenueCat y la pregunta
tras la compra", pero no recoge la opción B del 2026-10-31 (borrar los atributos ya enviados). Texto
propuesto para la sesión principal, si Anibal lo autoriza:
- ANTES: `que desactiva Crashlytics, el envío de atributos de medición a RevenueCat y la pregunta tras la compra.`
- DESPUÉS: `que desactiva Crashlytics, el envío de atributos de medición a RevenueCat y la pregunta tras la compra, y borra de RevenueCat los atributos ya enviados.`

No veo contradicción con `docs/brief-marketing.md`: los textos usan "datos técnicos" y "nunca tus
fotos", no "anónimos" ni "cero recopilación".

Fuera del alcance (para `growth`, solo aviso): la FAQ de la web ("¿Qué datos recoge la app?",
`astro/src/i18n/*.json`) podría añadir que se pueden desactivar en Ajustes. No es obligatorio.

---

## Fuentes
- Google Play, sección de seguridad de los datos: https://support.google.com/googleplay/android-developer/answer/10787469
- Apple, App Privacy Details: https://developer.apple.com/app-store/app-privacy-details/
- Apple, App Review Guidelines 5.1.1: https://developer.apple.com/app-store/review/guidelines/
- Firebase Crashlytics para Flutter, informes con consentimiento: https://firebase.google.com/docs/crashlytics/flutter/customize-crash-reports
- Firebase Crashlytics, referencia de iOS: https://firebase.google.com/docs/reference/ios/firebasecrashlytics/api/reference/Classes/FIRCrashlytics
- Firebase, datos para Google Play: https://firebase.google.com/docs/android/play-data-disclosure
- RevenueCat, atributos de cliente: https://www.revenuecat.com/docs/customers/customer-attributes
- RevenueCat, seguridad de datos de Google Play: https://www.revenuecat.com/docs/platform-resources/google-platform-resources/google-plays-data-safety

---

## H. `/delete-data/` · Restablecer App (añadido por hq el 2026-10-31, tras el informe T4e)

Comprobado en el código por `solopila`: el reset borra índice, datos de análisis y álbumes
de la app; no borra fotos; conserva ajustes (idioma, recordatorio, interruptor) y el
contador de búsquedas con cámara. Dos matices que la página no dice: en iPhone los álbumes
creados en Fotos siguen existiendo (solo salen de iSIMILAR) y la app vuelve a escanear la
galería justo después. Se publica junto con el resto de este borrador.

Apartado 1, punto "Restablecer la app" (sustituir la frase completa):
- EN DESPUÉS: `- Reset the app: open iSIMILAR > Settings > Reset App. This deletes the visual index and the analysis data, and undoes the albums created in the app. Your photos are not deleted. On iPhone, albums the app created in Photos stay there with their photos; delete them in Photos if you want. After the reset, the app scans your gallery again and builds a new index on the phone.`
- ES DESPUÉS: `- Restablecer la app: abre iSIMILAR > Ajustes > Restablecer App. Se borran el índice visual y los datos de análisis, y se deshacen los álbumes creados en la app. Tus fotos no se borran. En iPhone, los álbumes que la app creó en Fotos siguen allí con sus fotos; bórralos en Fotos si quieres. Después del restablecimiento, la app vuelve a escanear tu galería y crea un índice nuevo en el teléfono.`
- IT DESPUÉS: `- Reimpostare l'app: apri iSIMILAR > Impostazioni > Reimposta App. Vengono cancellati l'indice visivo e i dati di analisi, e vengono annullati gli album creati nell'app. Le tue foto non vengono eliminate. Su iPhone, gli album creati dall'app in Foto restano lì con le loro foto; eliminali in Foto se vuoi. Dopo il ripristino, l'app analizza di nuovo la galleria e crea un nuovo indice sul telefono.`
