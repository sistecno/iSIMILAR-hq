# Web isimilar.app · Fase 1 · Ajustes tras las respuestas de Anibal

Borrador de `growth` · 2026-10-23 · Estado: **pendiente de revisión de Anibal**
Corrige: `borradores/2026-10-21-web-fase1-textos.md` (en adelante, "borrador del 21").
Responde a: sección 10, "Respuestas de Anibal (2026-10-23)", puntos 1, 2, 3 y 8.
Aquí no se toca la web: cada cambio dice dónde va en el borrador del 21; se aplica en el montaje de Astro.

Convención: **Antes** = texto del borrador del 21 · **Ahora** = texto que lo sustituye.
Lo que no aparece aquí queda igual que en el borrador del 21.

---

## 1. FAQ "¿Es un limpiador de duplicados?"

### 1.1 Verificación (2026-10-23)

| Nombre que usa el texto | ¿Existe hoy con ese nombre? | Fuente oficial consultada |
|---|---|---|
| iPhone, Fotos: "Duplicates" (EN) | **Sí, pero hoy Apple lo llama "colección", no "álbum".** Guía del iPhone (selector hasta iOS 27): "The Photos app identifies duplicate photos and videos in your photo library in the Duplicates collection… Tap Collections. Tap Utilities, then tap Duplicates." Solo aparece si hay duplicados. El artículo 102260 (publicado 15-09-2025) aún dice "Duplicates album", desde iOS 16. | https://support.apple.com/en-us/guide/iphone/iph1978d9c23/ios · https://support.apple.com/en-us/102260 |
| iPhone, Fotos: "Duplicados" (ES) | **Sí**, como "la colección Duplicados". España: Colecciones › "Más ítems" › Duplicados. México: Colecciones › "Otros elementos" › Duplicados. | https://support.apple.com/es-es/guide/iphone/iph1978d9c23/ios · https://support.apple.com/es-mx/guide/iphone/iph1978d9c23/ios |
| iPhone, Fotos: "Duplicati" (IT) | **Sí**, como "la raccolta Duplicati" (Raccolte › Altro › Duplicati). | https://support.apple.com/it-it/guide/iphone/iph1978d9c23/ios |
| Files by Google, limpieza de duplicados | **Sí.** Menú › Limpiar › tarjeta "Duplicate files" / "Archivos duplicados" / "File duplicati". Los archivos van a la papelera. | https://support.google.com/files/answer/9764075?hl=en · `?hl=es` · `?hl=it` |
| "La galería de algunos fabricantes" | **Sí, al menos Samsung:** Galería › Clean out › "Delete duplicate pictures" (puede no aparecer si no hay duplicados). No he comprobado otros fabricantes; "algunos" es correcto con un solo caso verificado. | https://www.samsung.com/us/support/answer/ANS10002535/ |

**Ajuste por la verificación:** el texto de Anibal dice "el álbum Duplicados". Lo cambio a "la colección Duplicados" (ES), "Duplicates" sin sustantivo (EN, para no elegir entre "album" y "collection", que Apple usa en dos páginas distintas) y "la raccolta Duplicati" (IT), que es lo que dice hoy la guía oficial. En Android uso el nombre exacto de la tarjeta de Files by Google.

Nada negativo sobre esas herramientas: el texto solo dice que existen, que son gratuitas y que sirven para copias exactas.

⚠️ Contradicción detectada
- Documento: `docs/definicion-tecnica.md` · Límites conocidos dice: "Parecido por categoría, no por instancia. Una placa devuelve placas en general, no la placa concreta de un cliente."
- Fuente: borrador del 21 · sección 10, respuesta 8 (texto de Anibal) dice: "como distintos ángulos de la misma placa".
- Impacto: promete encontrar la misma placa (instancia). Es la frase que la FAQ "¿Encuentra una foto concreta?" desmiente, y la que el borrador del 21 ya quitó de `faq.a2` ("misma placa sugiere instancia"). Un asistente de IA puede citar las dos respuestas juntas.
- Opciones: A) ajustar la fuente al documento (propuesta abajo: "placas de distintas reparaciones") · B) Anibal revisa el documento
- Esperando decisión. Los textos de 1.2 ya usan la opción A.

### 1.2 Texto final

Dónde va: borrador del 21, sección 4.2 (EN), 4.3 (ES) y 4.4 (IT), pregunta sobre duplicados; y la misma respuesta en el avance de FAQ de la portada (sección 2.2, "Preguntas frecuentes", 2.ª pregunta) y en el JSON-LD `FAQPage`.

Pregunta: mantengo la del borrador del 21 (con "iSIMILAR" dentro) en lugar de "¿Es un limpiador de duplicados?": una pregunta con el nombre de la app se entiende sola cuando un asistente la cita. Si Anibal prefiere la suya, solo cambia el título.

**EN** — "Is iSIMILAR a duplicate photo cleaner?"
- Antes: No. It doesn't look for exact duplicates: it finds photos that look alike, such as the same kind of object, scene or document. If you only want to remove identical copies, iOS and Google already offer free duplicate cleanup.
- Ahora: No. For exact copies, your phone probably already has a free tool: on iPhone, Duplicates in the Photos app; on Android, the "Duplicate files" card in Files by Google, or the gallery app from some manufacturers. iSIMILAR does something different: it finds photos that look alike even when they aren't identical, like circuit boards from different repairs, products from the same shelf or screenshots with the same layout. With PRO, you can then move, share or delete them in bulk.

**ES** — "¿iSIMILAR es un limpiador de fotos duplicadas?"
- Antes: No. No busca duplicados exactos: encuentra fotos que se parecen, como el mismo tipo de objeto, escena o documento. Si solo quieres eliminar copias idénticas, iOS y Google ya ofrecen limpieza de duplicados gratis.
- Ahora: No. Para copias exactas, tu teléfono probablemente ya tiene una herramienta gratuita: en iPhone, la colección "Duplicados" de la app Fotos; en Android, la tarjeta "Archivos duplicados" de Files by Google o la galería de algunos fabricantes. iSIMILAR hace otra cosa: encuentra fotos que se parecen aunque no sean iguales, como placas de distintas reparaciones, productos del mismo estante o capturas con el mismo diseño. Después, con PRO, puedes moverlas, compartirlas o borrarlas en lote.

**IT** — "iSIMILAR è un'app per eliminare le foto doppie?"
- Antes: No. Non cerca i duplicati esatti: trova foto che si somigliano, come lo stesso tipo di oggetto, scena o documento. Se vuoi solo eliminare le copie identiche, iOS e Google offrono già la pulizia dei duplicati gratis.
- Ahora: No. Per le copie identiche, probabilmente il tuo telefono ha già uno strumento gratuito: su iPhone, la raccolta "Duplicati" dell'app Foto; su Android, la scheda "File duplicati" di Files by Google o la galleria di alcuni produttori. iSIMILAR fa un'altra cosa: trova le foto che si somigliano anche se non sono uguali, come schede elettroniche di riparazioni diverse, prodotti dello stesso scaffale o screenshot con la stessa grafica. Poi, con PRO, puoi spostarle, condividerle o eliminarle in blocco.

Cambios respecto al texto de Anibal: "álbum" → "colección" (nombre oficial actual); "Files by Google" → su tarjeta "Archivos duplicados"; "distintos ángulos de la misma placa" → "placas de distintas reparaciones" (contradicción de arriba); "te deja moverlas o borrarlas en lote" → "con PRO, puedes moverlas, compartirlas o borrarlas en lote" (el lote es siempre PRO; sin esa precisión la respuesta sugiere que es gratis). "Compartir" depende de la sección 2 (fecha de salida).

Riesgo: los nombres de menús cambian con cada versión de iOS/Android. Revisar estas tres URL cada vez que salga una versión mayor (septiembre para iOS).

---

## 2. Compartir en lote (PRO)

⚠️ Riesgo de calendario (no es contradicción con docs/): la web se sube hoy y compartir en lote llega "en la versión que se está terminando". Si la web sale antes de que la tienda apruebe esa versión, la web promete algo que la app publicada no hace (y un asistente de IA lo repetirá). Recomendación: montar los textos de esta sección en Astro pero publicarlos el día que la versión esté en las dos tiendas; hasta entonces, usar los textos del borrador del 21. Decide Anibal.

Nota para `monetizacion`: `docs/definicion-tecnica.md` (Medición) solo tiene `paywall_trigger` = `batch_delete` y `batch_album`. Si compartir en lote abre el muro de pago, falta un valor (p. ej. `batch_share`) para medirlo. Lo reporto, no lo decido.

No hay contradicción con docs/: el brief dice que las acciones en lote son siempre PRO; compartir en lote es una más. Los docs solo nombran "borrar o mover" como ejemplos.

### 2.1 Textos que cambian

**a) Portada · Precio · "Plan PRO · lista"** (borrador del 21, sección 2.2, tabla Precio). La misma lista se repite en "Cómo funciona" › "Free and PRO / Gratis y PRO / Gratis e PRO" (secciones 3.2-3.4), que remite a esta tabla.
- EN · Antes: 7-day free trial · Unlimited camera searches · Batch actions: delete or move hundreds of photos at once
- EN · Ahora: 7-day free trial · Unlimited camera searches · Batch actions: delete or move hundreds of photos at once, or share several together
- ES · Antes: 7 días de prueba gratis · Búsquedas con cámara ilimitadas · Acciones en lote: borra o mueve cientos de fotos de una vez
- ES · Ahora: 7 días de prueba gratis · Búsquedas con cámara ilimitadas · Acciones en lote: borra o mueve cientos de fotos de una vez, o comparte varias juntas
- IT · Antes: 7 giorni di prova gratuita · Ricerche con la fotocamera illimitate · Azioni in blocco: elimina o sposta centinaia di foto in una volta
- IT · Ahora: 7 giorni di prova gratuita · Ricerche con la fotocamera illimitate · Azioni in blocco: elimina o sposta centinaia di foto in una volta, oppure condividine diverse insieme

Por qué "varias" y no "cientos" al compartir: no sé cuántas fotos aceptan a la vez las apps de destino (WhatsApp, correo…). "Cientos" se queda para borrar y mover, que es lo que dice el brief.

**b) FAQ "What's free and what's PRO?" / "¿Qué es gratis y qué es PRO?" / "Cosa è gratis e cosa è PRO?"** (secciones 4.2-4.4). Solo cambia la frase de PRO; el resto igual.
- EN · Antes: PRO: unlimited camera searches and batch actions, such as deleting or moving hundreds of photos at once. There are no free batch actions.
- EN · Ahora: PRO: unlimited camera searches and batch actions: deleting or moving hundreds of photos at once, or sharing several together. There are no free batch actions.
- ES · Antes: PRO: búsquedas con cámara ilimitadas y acciones en lote, como borrar o mover cientos de fotos de una vez. No hay acciones en lote gratuitas.
- ES · Ahora: PRO: búsquedas con cámara ilimitadas y acciones en lote: borrar o mover cientos de fotos de una vez, o compartir varias juntas. No hay acciones en lote gratuitas.
- IT · Antes: PRO: ricerche con la fotocamera illimitate e azioni in blocco, come eliminare o spostare centinaia di foto in una volta. Non ci sono azioni in blocco gratuite.
- IT · Ahora: PRO: ricerche con la fotocamera illimitate e azioni in blocco: eliminare o spostare centinaia di foto in una volta, oppure condividerne diverse insieme. Non ci sono azioni in blocco gratuite.

**c) FAQ "What is iSIMILAR?" / "¿Qué es iSIMILAR?" / "Che cos'è iSIMILAR?"** (secciones 4.2-4.4), última frase. Es la respuesta que más citan los asistentes; conviene que nombre las tres acciones y que diga que el lote es PRO.
- EN · Antes: From the results you can search again, move photos to an album or delete them in bulk.
- EN · Ahora: From the results you can search again and, with PRO, move photos to an album, share them or delete them in bulk.
- ES · Antes: Desde los resultados puedes buscar de nuevo, mover fotos a un álbum o borrarlas en lote.
- ES · Ahora: Desde los resultados puedes buscar de nuevo y, con PRO, mover fotos a un álbum, compartirlas o borrarlas en lote.
- IT · Antes: Dai risultati puoi cercare di nuovo, spostare le foto in un album o eliminarle in blocco.
- IT · Ahora: Dai risultati puoi cercare di nuovo e, con PRO, spostare le foto in un album, condividerle o eliminarle in blocco.

**d) FAQ de duplicados**: ya incluye "compartir" (sección 1.2).

**e) JSON-LD**: `FAQPage` copia las respuestas de la FAQ, así que hereda b), c) y d) sin texto aparte. `SoftwareApplication` solo lleva `offers` (11.99 USD) en el borrador del 21: no cambia. Si en el montaje se añade `description` o `featureList`, que use la lista PRO de a).

### 2.2 Textos que no cambian (y por qué)
- Hero, entradilla ("Then move them to an album or delete them in bulk"): el brief define el pilar Ordena como mover y borrar; añadir compartir alarga la frase sin aportar al mensaje principal.
- "Cómo funciona" (resumen de portada), paso 3, y página "Cómo funciona", H2 4: ya dicen "share/comparte/condividi" y no hablan de lote.
- Metadatos (`title`, `description`, `og:*`) de las tres páginas: nombran mover y borrar como ejemplos; no mienten y añadir "compartir" rompe los límites de caracteres.
- Plan gratis: no añado "compartir una a una". Los docs solo dicen "borrado de una en una"; no sé si compartir o mover una sola foto es gratis. **Pregunta para Anibal:** ¿compartir y mover una foto suelta es gratis? Si lo es, conviene decirlo en la lista Gratis.

---

## 3. "Pantallas de teléfono" = fotos de pantallas físicas

Revisé todas las menciones. Las que hablan de la confusión con documentos dicen solo "phone screens / pantallas de teléfono / schermi di telefono", y un lector (o una IA) entiende "capturas de pantalla". Las cambio a "fotos de pantallas". Las menciones a capturas de WhatsApp (problema, tarjeta 3; perfil 2; FAQ de duplicados) hablan del segmento 2 del brief ("capturas repetidas") y son correctas: no cambian.

**a) Portada · "Lo que no hace", punto 5** (sección 2.2)
- EN · Antes: It gets it right about 80% of the time, and it mixes up documents and phone screens in about 1 in 5 cases. Review before you delete.
- EN · Ahora: It gets it right about 80% of the time, and in about 1 in 5 cases it mixes up documents with photos of phone screens. Review before you delete.
- ES · Antes: Acierta en torno al 80% de las veces y confunde documentos con pantallas de teléfono en uno de cada cinco casos, aproximadamente. Revisa antes de borrar.
- ES · Ahora: Acierta en torno al 80% de las veces y, en uno de cada cinco casos aproximadamente, confunde documentos con fotos de pantallas de teléfono. Revisa antes de borrar.
- IT · Antes: Ci azzecca circa 8 volte su 10 e in circa un caso su cinque confonde documenti e schermi di telefono. Controlla prima di eliminare.
- IT · Ahora: Ci azzecca circa 8 volte su 10 e in circa un caso su cinque confonde documenti e foto di schermi di telefono. Controlla prima di eliminare.

**b) "Cómo funciona" · "Limits you should know / Límites que conviene saber / Limiti da conoscere", 3.er punto** (secciones 3.2-3.4)
- EN · Antes: Documents and phone screens get mixed up in about 1 in 5 cases.
- EN · Ahora: Documents and photos of phone screens get mixed up in about 1 in 5 cases.
- ES · Antes: Confunde documentos con pantallas de teléfono en uno de cada cinco casos, aproximadamente.
- ES · Ahora: Confunde documentos con fotos de pantallas de teléfono en uno de cada cinco casos, aproximadamente.
- IT · Antes: In circa un caso su cinque confonde documenti e schermi di telefono.
- IT · Ahora: In circa un caso su cinque confonde documenti e foto di schermi di telefono.

**c) FAQ "Does it mix up documents with other photos?" / "¿Confunde documentos con otras fotos?" / "Confonde i documenti con altre foto?"** (secciones 4.2-4.4). Aquí sí aclaro la diferencia, porque es la respuesta que citará la IA.
- EN · Antes: Sometimes. Documents and phone screens get mixed up in about 1 in 5 cases. If you search from a document, expect some screens among the results, and the other way around.
- EN · Ahora: Sometimes. In about 1 in 5 cases it mixes up documents with photos of phone screens (pictures taken of a phone's display, not screenshots). If you search from a document, expect a few of those among the results, and the other way around.
- ES · Antes: A veces. Confunde documentos con pantallas de teléfono en uno de cada cinco casos, aproximadamente. Si buscas desde un documento, es normal que aparezca alguna pantalla entre los resultados, y al revés.
- ES · Ahora: A veces. En uno de cada cinco casos, aproximadamente, confunde documentos con fotos de pantallas de teléfono (fotos hechas a la pantalla de un móvil, no capturas de pantalla). Si buscas desde un documento, es normal que aparezca alguna de esas fotos entre los resultados, y al revés.
- IT · Antes: A volte. In circa un caso su cinque confonde documenti e schermi di telefono. Se cerchi partendo da un documento, è normale trovare qualche schermo tra i risultati, e viceversa.
- IT · Ahora: A volte. In circa un caso su cinque confonde documenti e foto di schermi di telefono (foto scattate al display di un telefono, non screenshot). Se cerchi partendo da un documento, è normale trovarne qualcuna tra i risultati, e viceversa.

Nota: no sé si las capturas de pantalla también se confunden con documentos; los docs no lo dicen. Por eso la aclaración solo afirma qué se midió, no que las capturas no se confundan.

**Riesgo de tono y legal (emails y contraseñas):** recomiendo **no mencionar nunca en público** que el técnico fotografía pantallas de clientes con emails o contraseñas.
- Legal: guardar credenciales de clientes en la galería personal es tratar datos personales de terceros (RGPD) sin medidas de seguridad; la web estaría animando a hacerlo. Además iSIMILAR no cifra ni protege la galería: puede leerse como si fuera un lugar seguro para contraseñas, que no lo es.
- Tono: contradice el pilar Privado y el ejemplo "enseñar el teléfono a un cliente sin miedo".
- Alternativa segura si se quiere el ejemplo: "fotos de pantallas de clientes: mensajes de error, ajustes, configuración" (ya cubierto por "error codes / códigos de error" en el perfil 1, así que no propongo cambio).
- En vídeos y capturas de tienda: tapar o desenfocar cualquier email o contraseña visible. Si algún día se quiere usar este caso, que lo revise antes `legal-tiendas`.

---

## 4. Funciona en modo avión desde la primera apertura

Ningún texto del borrador del 21 dice lo contrario: el escaneo, la búsqueda y la franja "Works in airplane mode" ya eran correctos. Solo añado "desde la primera vez" donde la duda era razonable, y corrijo un detalle que sí era impreciso: compartir manda las fotos a otra app, y esa app puede necesitar conexión.

**a) FAQ "Does it work without internet?" / "¿Funciona sin internet?" / "Funziona senza internet?"** (secciones 4.2-4.4)
- EN · Antes: Yes. Scanning, searching (from a photo or the camera) and acting on the results work offline, even in airplane mode. You need a connection to download the app and to buy or restore PRO.
- EN · Ahora: Yes, from the first time you open it. Scanning, searching (from a photo or the camera), deleting photos and moving them to albums work offline, even in airplane mode. You need a connection to download the app and to buy or restore PRO. When you share photos, the app you send them with may need one.
- ES · Antes: Sí. El escaneo, la búsqueda (desde una foto o con la cámara) y las acciones sobre los resultados funcionan sin conexión, también en modo avión. Necesitas conexión para descargar la app y para comprar o restaurar PRO.
- ES · Ahora: Sí, desde la primera vez que la abres. El escaneo, la búsqueda (desde una foto o con la cámara), el borrado y mover fotos a álbumes funcionan sin conexión, también en modo avión. Necesitas conexión para descargar la app y para comprar o restaurar PRO. Al compartir fotos, la app a la que las envías puede necesitarla.
- IT · Antes: Sì. Scansione, ricerca (da una foto o con la fotocamera) e azioni sui risultati funzionano offline, anche in modalità aereo. La connessione serve per scaricare l'app e per acquistare o ripristinare PRO.
- IT · Ahora: Sì, fin dalla prima apertura. Scansione, ricerca (da una foto o con la fotocamera), eliminazione e spostamento delle foto negli album funzionano offline, anche in modalità aereo. La connessione serve per scaricare l'app e per acquistare o ripristinare PRO. Quando condividi le foto, l'app con cui le invii potrebbe averne bisogno.

**b) "Cómo funciona", H2 1, primera frase** (secciones 3.2-3.4). Cambio opcional, recomendado.
- EN · Antes: The first time you open the app, it scans your gallery once.
- EN · Ahora: The first time you open the app, it scans your gallery once, even without a connection.
- ES · Antes: La primera vez que abres la app, escanea tu galería una sola vez.
- ES · Ahora: La primera vez que abres la app, escanea tu galería una sola vez, también sin conexión.
- IT · Antes: La prima volta che apri l'app, analizza la galleria una sola volta.
- IT · Ahora: La prima volta che apri l'app, analizza la galleria una sola volta, anche senza connessione.

No escribo "todo funciona sin conexión": el recordatorio semanal usa Firebase Cloud Messaging (definición técnica, Datos y privacidad), y no puedo confirmar que se active sin red.

---

## 5. Revisión con `tono-de-marca`

| Frase | Problema | Regla | Versión entregada |
|---|---|---|---|
| "distintos ángulos de la misma placa" (texto de Anibal) | Promete instancia | Definición técnica, Límites: categoría, no instancia | "placas de distintas reparaciones" (contradicción en 1.1) |
| "te deja moverlas o borrarlas en lote" (texto de Anibal) | Sugiere lote gratis | Brief, Precio: lote siempre PRO | "con PRO, puedes moverlas, compartirlas o borrarlas en lote" |
| "el álbum Duplicados" (texto de Anibal) | Nombre no actual en la guía oficial | Verificación 1.1 | "la colección Duplicados" / "Duplicates" / "la raccolta Duplicati" |
| "share several together" | Sin cifra | Brief: sin promesas no verificables | "varias", no "cientos" |
| "acting on the results work offline" | Compartir puede necesitar red en la app de destino | Brief: "Funciona sin conexión, en modo avión" (permitido) sin extenderlo | Se nombran borrar y mover; compartir, con salvedad |
| "photos of phone screens (… not screenshots)" | Ninguno; aclara | Definición técnica, Límites | Permitido |

Pilares: duplicados → Encuentra + Ordena; PRO → Ordena; modo avión → Privado. Sin "magia", "el primero", "exacta", cifras sin fuente, "5 free actions" ni nada negativo sobre Apple, Google o Samsung. Precio y PRO idénticos al brief.

**Veredicto: apto con cambios** — pendiente de la contradicción de 1.1, de la fecha de salida de compartir en lote (sección 2) y de la pregunta sobre acciones sueltas gratis (2.2).

---

## 6. Resumen

- FAQ de duplicados: entregada en EN/ES/IT. Verificado hoy en fuentes oficiales: Apple (Duplicados/Duplicates/Duplicati), Files by Google ("Archivos duplicados") y Samsung Galería ("Delete duplicate pictures").
- Cambio por la verificación: Apple ya lo llama "colección" (raccolta), no "álbum"; en EN no uso sustantivo porque Apple usa ambos en páginas distintas.
- Contradicción: "distintos ángulos de la misma placa" promete instancia; propongo "placas de distintas reparaciones".
- Compartir en lote (PRO): cambian lista PRO, FAQ "gratis/PRO", FAQ "¿Qué es?" y FAQ de duplicados; JSON-LD `FAQPage` lo hereda.
- Riesgo: si la web sale antes que la versión de la app, promete una función que no existe. Falta un valor `batch_share` en la medición.
- Pantallas: 3 textos × 3 idiomas pasan a "fotos de pantallas"; los de capturas de WhatsApp se quedan. No mencionar contraseñas de clientes en público (RGPD y tono).
- Modo avión: FAQ y "Cómo funciona" dicen "desde la primera vez"; compartir lleva salvedad.
- No pude verificar: otros fabricantes aparte de Samsung; si capturas de pantalla también se confunden con documentos; si el recordatorio semanal funciona sin red; si mover o compartir una foto suelta es gratis.
