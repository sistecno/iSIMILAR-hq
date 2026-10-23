# Web isimilar.app · Fase 1 · Textos, metadatos y mapa de páginas

Borrador de `growth` · 2026-10-21 · Estado: **pendiente de revisión de Anibal**
Base: `decisiones/2026-10-21-web-astro-seo.md` (Astro estático, `/` en inglés, `/es/`, `/it/`, opción A).
Fuentes: `docs/brief-marketing.md`, `docs/guia-estrategica.md`, `docs/definicion-tecnica.md`.
Web de referencia (solo lectura): `solopila_landingPAGE/web/index.html` y `web/i18n.js`.

Dónde va: todo esto se monta en la Fase 2, en una sesión abierta en `solopila_landingPAGE/`.
Aquí no se toca la web.

---

## 0. Antes de leer: lo que cambia respecto a la web actual

- Una URL por idioma con el texto escrito en el HTML (hoy es una sola URL y el idioma se cambia con JavaScript).
- Fuera: "el primero", "0,5 s", "facturas", "gratis para siempre" a secas, "15 GB", "cero datos",
  "magia", la comparativa con Google Fotos y Apple Fotos y el precio 12,99 USD.
- Nuevo: un bloque "Lo que iSIMILAR no hace" en la portada y una página de preguntas frecuentes
  pensada para que los asistentes de IA la citen.
- Sin analítica web con cookies: una app que vende privacidad no debería poner un rastreador en su web.
  La medición se hace con Search Console y con enlaces de campaña a las tiendas (ver sección 7).

---

## 1. Mapa de páginas de la Fase 1

| Página | EN | ES | IT | Objetivo | Búsqueda principal que ataca |
|---|---|---|---|---|---|
| Inicio | `/` | `/es/` | `/it/` | Que quien llega entienda en 5 segundos qué hace, qué no hace y cuánto cuesta, y vaya a la tienda | EN "find similar photos" · ES "buscar fotos parecidas" · IT "trovare foto simili" |
| Cómo funciona | `/how-it-works/` | `/es/como-funciona/` | `/it/come-funziona/` | Explicar el proceso y los límites con texto claro; dar contexto a buscadores e IA | EN "search photos by image offline" · ES "buscar fotos por imagen sin internet" · IT "cercare foto per immagine" |
| Preguntas frecuentes | `/faq/` | `/es/preguntas-frecuentes/` | `/it/domande-frequenti/` | Respuestas citables por ChatGPT, Perplexity, Gemini y Copilot; desmentir el error de privacidad que repite ChatGPT | Preguntas tipo "does iSIMILAR upload photos", "iSIMILAR vs duplicate cleaner", "app para encontrar fotos parecidas sin internet" |
| Privacidad (legal-tiendas) | `/privacy` | (lo decide legal-tiendas) | (lo decide legal-tiendas) | Solo enlace en el pie | — |
| Términos (legal-tiendas) | `/terms` | (lo decide legal-tiendas) | (lo decide legal-tiendas) | Solo enlace en el pie | — |

Notas técnicas para la Fase 2 (no son textos, son requisitos para que el texto cuente):
- `hreflang`: `en` → `/…`, `es` → `/es/…`, `it` → `/it/…`, `x-default` → `/…`. Usar `es` sin país
  (sirve a España y Latam) e `it`.
- `canonical` propio en cada página e idioma. `/en/` → 301 a `/` (decidido).
- Enlace de App Store neutro, sin `/us/`: `https://apps.apple.com/app/id6738889078`
  (hoy `index.html` línea 198 usa `/us/`). Con token de campaña (sección 7).
- Datos estructurados: `SoftwareApplication` (con `offers` 11.99 USD) en las tres portadas y
  `FAQPage` en las preguntas frecuentes. No esperar resultado enriquecido de FAQ en Google
  (lo limitó en 2023 a webs de gobierno y salud); sirve como texto estructurado para buscadores e IA.
- `og:locale`: `en_US`, `es_LA` (con `og:locale:alternate` `es_ES`), `it_IT`.
- Imagen `og:image`: reutilizar `isimilar-preview.jpg` solo si no muestra "5 free actions",
  "el primero" ni precios antiguos. No puedo confirmarlo: no he visto la imagen.

---

## 2. Página de inicio

### 2.1 Metadatos

| Campo | EN (`/`) | ES (`/es/`) | IT (`/it/`) |
|---|---|---|---|
| `<title>` | iSIMILAR: Find Similar Photos on Your Phone, Offline (52) | iSIMILAR: busca fotos parecidas en tu galería sin internet (58) | iSIMILAR: trova foto simili nella galleria, senza internet (58) |
| meta description | Pick a photo or point your camera and iSIMILAR finds the ones that look alike in your gallery. Works offline; your photos never leave your phone. (145) | Elige una foto o apunta la cámara: iSIMILAR encuentra las que se parecen en tu galería. Sin internet y sin subir tus fotos. (123) | Scegli una foto o inquadra un oggetto: iSIMILAR trova in galleria le foto simili. Funziona offline: le tue foto restano sul telefono. (133) |
| og:title | iSIMILAR: find similar photos by looking, not typing | iSIMILAR: encuentra fotos parecidas mirando, no escribiendo | iSIMILAR: trova foto simili guardando, non scrivendo |
| og:description | Pick a photo or point your camera. iSIMILAR finds the ones that look alike in your gallery, offline. Your photos never leave your phone. | Elige una foto o apunta la cámara. iSIMILAR encuentra las que se parecen en tu galería, sin internet. Tus fotos nunca salen del teléfono. | Scegli una foto o inquadra un oggetto. iSIMILAR trova le foto simili nella tua galleria, senza internet. Le tue foto non lasciano mai il telefono. |

(Entre paréntesis, caracteres contados a mano, espacios incluidos.)

### 2.2 Textos por sección

#### Hero

| Elemento | EN | ES | IT |
|---|---|---|---|
| Etiqueta superior | Offline · No cloud · No account | Sin internet · Sin nube · Sin cuenta | Offline · Niente cloud · Nessun account |
| H1 | Find similar photos by looking, not typing | Encuentra fotos parecidas mirando, no escribiendo | Trova foto simili guardando, non scrivendo |
| Entradilla | Pick a photo or point your camera at something. iSIMILAR finds the photos in your gallery that look like it, without internet and without uploading your photos. Then move them to an album or delete them in bulk. | Elige una foto o apunta la cámara a algo. iSIMILAR encuentra en tu galería las fotos que se le parecen, sin internet y sin subir tus fotos. Después, las mueves a un álbum o las borras en lote. | Scegli una foto o inquadra un oggetto con la fotocamera. iSIMILAR trova nella tua galleria le foto simili, senza internet e senza caricare le tue foto da nessuna parte. Poi le sposti in un album o le elimini in blocco. |
| Botones tienda | Download on the App Store · Get it on Google Play | Descárgala en la App Store · Disponible en Google Play | Scarica su App Store · Disponibile su Google Play |
| Línea de confianza | Free search, forever · No account · Works in airplane mode | Búsqueda gratis para siempre · Sin cuenta · Funciona en modo avión | Ricerca gratis per sempre · Nessun account · Funziona in modalità aereo |
| Alt de la imagen | iSIMILAR on a phone: a circuit board photo and a grid of similar photos found in the gallery | iSIMILAR en un teléfono: la foto de una placa y una cuadrícula de fotos parecidas encontradas en la galería | iSIMILAR su un telefono: la foto di una scheda elettronica e una griglia di foto simili trovate in galleria |

Nota: el alt debe describir la imagen real. Si la imagen no es una placa, se cambia el alt, no la imagen.

#### Franja de datos (sustituye a "< 0.5s · ~23 MB · 0 servidores · 0 cuentas", `index.html` línea 136)

| EN | ES | IT |
|---|---|---|
| Under 1 second per search | Menos de 1 segundo por búsqueda | Meno di 1 secondo per ricerca |
| Works in airplane mode | Funciona en modo avión | Funziona in modalità aereo |
| No account needed | Sin cuenta | Nessun account |
| Photos stay on your phone | Tus fotos no salen del teléfono | Le foto restano sul telefono |

#### El problema

| Elemento | EN | ES | IT |
|---|---|---|---|
| H2 | Your work photos are mixed with your life | Tus fotos de trabajo, mezcladas con tu vida | Le foto di lavoro mescolate alla tua vita |
| Tarjeta 1 título | Work and family in one gallery | Trabajo y familia en la misma galería | Lavoro e famiglia nella stessa galleria |
| Tarjeta 1 texto | Circuit boards, error codes, pipes, repairs, scattered among photos of your kids and your holidays. | Placas, códigos de error, tuberías y reparaciones repartidas entre las fotos de tus hijos y tus vacaciones. | Schede elettroniche, codici di errore, tubature e riparazioni sparse tra le foto dei tuoi figli e delle vacanze. |
| Tarjeta 2 título | Showing your phone to a client | Enseñar el teléfono a un cliente | Mostrare il telefono a un cliente |
| Tarjeta 2 texto | You hand over your phone to show a repair, and one swipe later they're looking at your personal photos. | Le pasas el teléfono para mostrarle una reparación y basta deslizar el dedo para que vea tus fotos personales. | Gli passi il telefono per fargli vedere una riparazione e basta uno scorrimento perché finisca sulle tue foto personali. |
| Tarjeta 3 título | Hundreds of near-identical images | Cientos de imágenes casi iguales | Centinaia di immagini quasi uguali |
| Tarjeta 3 texto | WhatsApp memes, good-morning images and screenshots, or the same product photographed again and again. | Memes, saludos de buenos días y capturas de WhatsApp, o el mismo producto fotografiado una y otra vez. | Meme, buongiorno e screenshot di WhatsApp, o lo stesso prodotto fotografato più e più volte. |

#### Cómo funciona (resumen)

| Elemento | EN | ES | IT |
|---|---|---|---|
| H2 | How it works | Cómo funciona | Come funziona |
| Paso 1 título | Pick a base photo | Elige una foto base | Scegli una foto di partenza |
| Paso 1 texto | Choose one from your gallery or take one with the camera. | Una de tu galería o una nueva con la cámara. | Dalla galleria, oppure scattane una con la fotocamera. |
| Paso 2 título | See what looks alike | Mira lo que se parece | Guarda cosa le somiglia |
| Paso 2 texto | iSIMILAR compares shape, texture, color and composition on your phone and shows the most similar photos first. Tap any result to search again from it. | iSIMILAR compara forma, textura, color y composición dentro de tu teléfono y muestra primero las más parecidas. Toca cualquier resultado para buscar de nuevo desde ahí. | iSIMILAR confronta forma, texture, colore e composizione direttamente sul telefono e mostra prima le più simili. Tocca un risultato per ripartire con una nuova ricerca. |
| Paso 3 título | Decide what to do | Decide qué hacer | Decidi tu cosa fare |
| Paso 3 texto | Move the results to an album, share them or delete them. You review and confirm every action. | Mueve los resultados a un álbum, compártelos o bórralos. Tú revisas y confirmas cada acción. | Sposta i risultati in un album, condividili o eliminali. Ogni azione la controlli e la confermi tu. |
| Enlace | See how it works in detail → | Ver cómo funciona en detalle → | Scopri come funziona nel dettaglio → |

#### Para quién

| Elemento | EN | ES | IT |
|---|---|---|---|
| H2 | For people who photograph the same kind of thing again and again | Para quien fotografía una y otra vez el mismo tipo de cosa | Per chi fotografa sempre lo stesso tipo di cose |
| Perfil 1 título | Repair technicians and trades | Técnicos de reparación y oficios | Tecnici e artigiani |
| Perfil 1 texto | Phone and laptop repair, appliances, HVAC, mechanics. Separate your work photos in minutes: gather them in an album, away from your personal ones. | Reparación de teléfonos y portátiles, electrodomésticos, climatización, mecánica. Separa tus fotos de trabajo en minutos: júntalas en un álbum, lejos de las personales. | Riparazione di smartphone e portatili, elettrodomestici, climatizzazione, officine. Separa le foto di lavoro in pochi minuti: raccoglile in un album, lontano da quelle personali. |
| Perfil 2 título | A gallery full of WhatsApp | Una galería llena de WhatsApp | Una galleria piena di WhatsApp |
| Perfil 2 texto | Pick one meme or screenshot and delete the ones that look like it in one go. | Elige un meme o una captura y borra de una vez los que se le parecen. | Scegli un meme o uno screenshot ed elimina in un colpo solo quelli simili. |
| Perfil 3 título | Everyday photos that repeat | Fotos repetidas del día a día | Foto ripetute di tutti i giorni |
| Perfil 3 texto | Supermarket products you send home, clothes, receipts with the same layout. Search from one and keep going from any result. | Productos del supermercado que envías a la familia, ropa, recibos con el mismo formato. Busca desde una y sigue en cadena desde cualquier resultado. | Prodotti del supermercato mandati in famiglia, vestiti, scontrini con lo stesso formato. Parti da una foto e continua la ricerca da qualsiasi risultato. |

#### Lo que no hace (bloque nuevo)

| Elemento | EN | ES | IT |
|---|---|---|---|
| H2 | What iSIMILAR doesn't do | Lo que iSIMILAR no hace | Cosa iSIMILAR non fa |
| 1 | It doesn't look for exact duplicates: it finds what looks alike, not what's identical. | No busca duplicados exactos: encuentra lo parecido, no lo idéntico. | Non cerca i duplicati esatti: trova ciò che si somiglia, non ciò che è identico. |
| 2 | It doesn't sort your photos on its own: you choose and confirm. | No ordena tus fotos por su cuenta: tú eliges y confirmas. | Non riordina le foto da sola: scegli e confermi tu. |
| 3 | It isn't Google Lens: it doesn't identify objects or search the internet. | No es Google Lens: no identifica objetos ni busca en internet. | Non è Google Lens: non riconosce gli oggetti e non cerca su internet. |
| 4 | It doesn't search by text, date or location. | No busca por texto, fecha ni ubicación. | Non cerca per testo, data o luogo. |
| 5 | It gets it right about 80% of the time, and it mixes up documents and phone screens in about 1 in 5 cases. Review before you delete. | Acierta en torno al 80% de las veces y confunde documentos con pantallas de teléfono en uno de cada cinco casos, aproximadamente. Revisa antes de borrar. | Ci azzecca circa 8 volte su 10 e in circa un caso su cinque confonde documenti e schermi di telefono. Controlla prima di eliminare. |

#### Precio

| Elemento | EN | ES | IT |
|---|---|---|---|
| H2 | Searching is free. Batch actions are PRO. | Buscar es gratis. Ordenar en lote, con PRO. | Cercare è gratis. Per riordinare in blocco c'è PRO. |
| Plan gratis · título | Free | Gratis | Gratis |
| Plan gratis · lista | Gallery scan · Unlimited searches from your saved photos · 5 camera searches · Delete photos one at a time | Escaneo de la galería · Búsquedas ilimitadas desde tus fotos guardadas · 5 búsquedas con la cámara · Borrado de una en una | Scansione della galleria · Ricerche illimitate dalle foto salvate · 5 ricerche con la fotocamera · Eliminazione di una foto alla volta |
| Plan PRO · título | PRO | PRO | PRO |
| Plan PRO · precio | $11.99/year in the US · €12/year in the eurozone | 12 €/año en la zona euro · 11,99 USD/año en EE. UU. | 12 € all'anno |
| Plan PRO · lista | 7-day free trial · Unlimited camera searches · Batch actions: delete or move hundreds of photos at once | 7 días de prueba gratis · Búsquedas con cámara ilimitadas · Acciones en lote: borra o mueve cientos de fotos de una vez | 7 giorni di prova gratuita · Ricerche con la fotocamera illimitate · Azioni in blocco: elimina o sposta centinaia di foto in una volta |
| Botón | Start the 7-day free trial | Empezar la prueba de 7 días | Inizia la prova di 7 giorni |
| Nota | In other countries, the App Store or Google Play shows the local price before you pay. If you don't cancel before the trial ends, the annual subscription is charged. You can cancel in your store's subscription settings. | En otros países, la App Store o Google Play muestran el precio local antes de pagar. Si no cancelas antes de que termine la prueba, se cobra la suscripción anual. Puedes cancelarla en los ajustes de suscripciones de tu tienda. | Fuori dall'area euro, l'App Store o Google Play mostrano il prezzo locale prima del pagamento (negli Stati Uniti 11,99 USD). Se non disdici prima della fine della prova, viene addebitato l'abbonamento annuale. Puoi disdirlo dalle impostazioni abbonamenti dello store. |

#### Preguntas frecuentes (avance en portada: 3 preguntas, respuestas idénticas a las de la página FAQ)

EN: "Do my photos leave my phone?" · "Is iSIMILAR a duplicate photo cleaner?" · "How accurate is it?" · Enlace: "All questions →"
ES: "¿Mis fotos salen del teléfono?" · "¿iSIMILAR es un limpiador de fotos duplicadas?" · "¿Cuánto acierta?" · Enlace: "Todas las preguntas →"
IT: "Le mie foto escono dal telefono?" · "iSIMILAR è un'app per eliminare le foto doppie?" · "Quanto è precisa?" · Enlace: "Tutte le domande →"

#### Cierre

| Elemento | EN | ES | IT |
|---|---|---|---|
| H2 | Try it with your own gallery | Pruébala con tu propia galería | Provala con la tua galleria |
| Subtítulo | Searching is free. No account. Works offline. | Buscar es gratis. Sin cuenta. Sin internet. | Cercare è gratis. Nessun account. Senza internet. |
| Texto QR | Scan with your phone to open your app store. | Escanéalo con tu teléfono para abrir tu tienda de apps. | Inquadralo con il telefono per aprire il tuo store. |

#### Pie (común a todas las páginas)

| EN | ES | IT |
|---|---|---|
| Privacy Policy → `/privacy` | Política de privacidad → `/privacy` | Informativa sulla privacy → `/privacy` |
| Terms of Use → `/terms` | Términos de uso → `/terms` | Termini d'uso → `/terms` |
| info@isimilar.app · © 2026 iSIMILAR | info@isimilar.app · © 2026 iSIMILAR | info@isimilar.app · © 2026 iSIMILAR |
| Selector: English · Español · Italiano | igual | igual |

Hasta que legal-tiendas publique `/privacy` y `/terms`, el pie no puede enlazar a páginas vacías:
o se publican a la vez, o el pie apunta temporalmente a las URL de Notion (decisión de Anibal).

---

## 3. Página "Cómo funciona"

### 3.1 Metadatos

| Campo | EN (`/how-it-works/`) | ES (`/es/como-funciona/`) | IT (`/it/come-funziona/`) |
|---|---|---|---|
| `<title>` | How iSIMILAR Works: Search Your Photos by Image, Offline (56) | Cómo funciona iSIMILAR: busca fotos por imagen sin internet (59) | Come funziona iSIMILAR: cerca foto per immagine, offline (56) |
| meta description | Choose a base photo or use the camera. iSIMILAR compares shape, texture, color and composition on your phone and lets you move or delete results in bulk. (153) | Elige una foto base o usa la cámara. iSIMILAR compara forma, textura, color y composición en tu teléfono, y luego mueves o borras los resultados en lote. (153) | Scegli una foto di partenza o usa la fotocamera. iSIMILAR confronta forma, texture, colore e composizione sul telefono; poi sposti o elimini in blocco. (151) |
| og:title | How iSIMILAR searches your photos by image | Cómo busca iSIMILAR tus fotos por imagen | Come iSIMILAR cerca le tue foto per immagine |
| og:description | One scan, then search from a photo or the camera, offline. Move or delete the results in bulk. Your photos never leave your phone. | Un escaneo y luego busca desde una foto o la cámara, sin internet. Mueve o borra los resultados en lote. Tus fotos nunca salen del teléfono. | Una scansione, poi cerchi da una foto o dalla fotocamera, senza internet. Sposti o elimini i risultati in blocco. Le foto restano sul telefono. |

### 3.2 Textos — EN

**H1:** How iSIMILAR searches your photos by image

**Intro:** iSIMILAR is a private visual search engine for your phone's gallery. You give it a photo and it shows you the ones that look like it. Everything runs on the phone, without internet.

**H2 · 1. One scan, at the start**
The first time you open the app, it scans your gallery once. On an iPhone 13 with 15,000 photos it takes 2.5 to 3 minutes; we haven't measured it yet on a mid-range Android phone. After that, it only processes new photos, and if the scan is interrupted it picks up where it left off. Your originals aren't copied or moved: the app keeps a small visual fingerprint of each photo, on the phone.

**H2 · 2. Search from a photo or the camera**
Pick any photo from your gallery, or point the camera at something in front of you: a circuit board, a product on the shelf, a receipt. Results appear in under a second, sorted from most to least similar.

**H2 · 3. Keep searching from any result**
Tap any result to start a new search from it. It's useful when what you're after looks a bit different from your first photo.

**H2 · 4. Act on the results**
Delete, move to a new or existing album, or share. You always see a preview and confirm before anything happens. Photos you move to an album stop showing up in later searches, so each search shows what's left to sort. On iPhone you can also remove a photo from an album without deleting it, and delete albums from the app.

**H2 · 5. An optional weekly reminder**
If you turn it on, iSIMILAR reminds you once a week to review your new photos.

**H2 · What it compares**
Shape, texture, color and composition. It doesn't recognize objects by name, faces or text. That's why it works best with photos taken in similar conditions: same angle, same light, same background.

**H2 · Limits you should know**
- It finds by category, not by instance: a photo of a circuit board returns circuit boards in general, not one specific client's board.
- It gets it right about 80% of the time.
- Documents and phone screens get mixed up in about 1 in 5 cases.
- It doesn't learn from your gallery.
- It doesn't search by text, date, location or client.
- It doesn't sync between devices.

**H2 · Privacy**
Your photos and their thumbnails never leave the phone. The visual fingerprints are computed and stored only on the device. The app sends technical data on purchases, usage and errors, never photos or gallery content. Details in the Privacy Policy.

**H2 · Free and PRO** — (misma tabla que en la portada) + botón "Start the 7-day free trial".

### 3.3 Textos — ES

**H1:** Cómo busca iSIMILAR tus fotos por imagen

**Intro:** iSIMILAR es un buscador visual privado para la galería del teléfono. Le das una foto y te muestra las que se le parecen. Todo ocurre dentro del teléfono, sin internet.

**H2 · 1. Un escaneo, al principio**
La primera vez que abres la app, escanea tu galería una sola vez. En un iPhone 13 con 15.000 fotos tarda entre 2,5 y 3 minutos; en un Android de gama media todavía no lo hemos medido. Después solo procesa las fotos nuevas, y si el escaneo se interrumpe, sigue desde donde se quedó. Tus originales no se copian ni se mueven: la app guarda una pequeña huella visual de cada foto, dentro del teléfono.

**H2 · 2. Busca desde una foto o con la cámara**
Elige cualquier foto de tu galería o apunta la cámara a lo que tengas delante: una placa, un producto en el estante, un recibo. Los resultados aparecen en menos de un segundo, ordenados de más a menos parecidos.

**H2 · 3. Sigue buscando desde cualquier resultado**
Toca un resultado para lanzar una búsqueda nueva desde él. Sirve cuando lo que buscas se ve un poco distinto de tu primera foto.

**H2 · 4. Actúa sobre los resultados**
Borra, mueve a un álbum nuevo o existente, o comparte. Siempre ves una vista previa y confirmas antes de que pase nada. Las fotos que mueves a un álbum dejan de aparecer en búsquedas posteriores, así cada búsqueda muestra lo que te queda por ordenar. En iPhone también puedes quitar una foto de un álbum sin borrarla y borrar álbumes desde la app.

**H2 · 5. Un recordatorio semanal, si lo quieres**
Si lo activas, iSIMILAR te recuerda una vez por semana revisar tus fotos nuevas.

**H2 · Qué compara**
Forma, textura, color y composición. No reconoce objetos por su nombre, ni caras, ni texto. Por eso funciona mejor con fotos hechas en condiciones parecidas: mismo ángulo, misma luz, mismo fondo.

**H2 · Límites que conviene saber**
- Encuentra por categoría, no por instancia: la foto de una placa devuelve placas en general, no la placa concreta de un cliente.
- Acierta en torno al 80% de las veces.
- Confunde documentos con pantallas de teléfono en uno de cada cinco casos, aproximadamente.
- No aprende de tu galería.
- No busca por texto, fecha, ubicación ni cliente.
- No sincroniza entre dispositivos.

**H2 · Privacidad**
Tus fotos y sus miniaturas nunca salen del teléfono. Las huellas visuales se calculan y se guardan solo en el dispositivo. La app envía datos técnicos de compras, uso y errores, sin fotos ni contenido de la galería. Los detalles, en la Política de privacidad.

**H2 · Gratis y PRO** — (misma tabla que en la portada) + botón "Empezar la prueba de 7 días".

### 3.4 Textos — IT

**H1:** Come iSIMILAR cerca le tue foto per immagine

**Intro:** iSIMILAR è un motore di ricerca visiva privato per la galleria del telefono. Gli dai una foto e ti mostra quelle simili. Tutto avviene sul telefono, senza internet.

**H2 · 1. Una scansione, all'inizio**
La prima volta che apri l'app, analizza la galleria una sola volta. Su un iPhone 13 con 15.000 foto ci vogliono da 2,5 a 3 minuti; su un Android di fascia media non l'abbiamo ancora misurato. Dopo elabora solo le foto nuove e, se la scansione si interrompe, riprende da dove si era fermata. Gli originali non vengono copiati né spostati: l'app salva sul telefono una piccola impronta visiva di ogni foto.

**H2 · 2. Cerca da una foto o con la fotocamera**
Scegli una foto dalla galleria oppure inquadra quello che hai davanti: una scheda elettronica, un prodotto sullo scaffale, uno scontrino. I risultati arrivano in meno di un secondo, dal più simile al meno simile.

**H2 · 3. Continua a cercare da qualsiasi risultato**
Tocca un risultato per avviare una nuova ricerca da lì. Utile quando quello che cerchi è un po' diverso dalla prima foto.

**H2 · 4. Agisci sui risultati**
Elimina, sposta in un album nuovo o esistente, oppure condividi. Vedi sempre un'anteprima e confermi prima che succeda qualcosa. Le foto che sposti in un album non compaiono più nelle ricerche successive: così ogni ricerca ti mostra quello che resta da sistemare. Su iPhone puoi anche togliere una foto da un album senza eliminarla ed eliminare album dall'app.

**H2 · 5. Un promemoria settimanale, se vuoi**
Se lo attivi, iSIMILAR ti ricorda una volta a settimana di controllare le foto nuove.

**H2 · Cosa confronta**
Forma, texture, colore e composizione. Non riconosce gli oggetti per nome, né volti, né testo. Per questo funziona meglio con foto scattate in condizioni simili: stessa angolazione, stessa luce, stesso sfondo.

**H2 · Limiti da conoscere**
- Trova per categoria, non il singolo oggetto: la foto di una scheda elettronica restituisce schede in generale, non quella di un cliente preciso.
- Ci azzecca circa 8 volte su 10.
- In circa un caso su cinque confonde documenti e schermi di telefono.
- Non impara dalla tua galleria.
- Non cerca per testo, data, luogo o cliente.
- Non sincronizza tra dispositivi.

**H2 · Privacy**
Le tue foto e le loro miniature non lasciano mai il telefono. Le impronte visive vengono calcolate e salvate solo sul dispositivo. L'app invia dati tecnici su acquisti, utilizzo ed errori, mai foto o contenuti della galleria. I dettagli sono nell'Informativa sulla privacy.

**H2 · Gratis e PRO** — (stessa tabella della home) + pulsante "Inizia la prova di 7 giorni".

---

## 4. Página de preguntas frecuentes

Criterio: la primera frase de cada respuesta contesta sola ("Sí", "No", un dato). Así un asistente
puede citarla sin contexto. Las mismas preguntas en los tres idiomas, para que la IA dé la misma
respuesta en cada uno. Se marcan con **[LT]** las respuestas que debe revisar legal-tiendas.

### 4.1 Metadatos

| Campo | EN (`/faq/`) | ES (`/es/preguntas-frecuentes/`) | IT (`/it/domande-frequenti/`) |
|---|---|---|---|
| `<title>` | iSIMILAR FAQ: Privacy, Pricing and What the App Can't Do (56) | iSIMILAR: preguntas frecuentes, privacidad, precio y límites (60) | iSIMILAR: domande frequenti su privacy, prezzo e limiti (55) |
| meta description | Straight answers about iSIMILAR: does it upload photos, does it find exact duplicates, how accurate is it, what's free and what PRO costs. (138) | Respuestas claras sobre iSIMILAR: si sube tus fotos, si busca duplicados exactos, cuánto acierta, qué es gratis y cuánto cuesta PRO. (132) | Risposte chiare su iSIMILAR: carica le tue foto? Trova i duplicati esatti? Quanto è precisa? Cosa è gratis e quanto costa PRO? (126) |
| og:title | iSIMILAR: straight answers, including what it can't do | iSIMILAR: respuestas claras, también sobre lo que no hace | iSIMILAR: risposte chiare, anche su cosa non fa |
| og:description | Privacy, offline use, accuracy, duplicates, price and free trial. What iSIMILAR does and doesn't do, in plain words. | Privacidad, uso sin internet, acierto, duplicados, precio y prueba gratis. Lo que iSIMILAR hace y no hace, sin rodeos. | Privacy, uso offline, precisione, duplicati, prezzo e prova gratuita. Cosa fa e cosa non fa iSIMILAR, senza giri di parole. |
| H1 | Frequently asked questions about iSIMILAR | Preguntas frecuentes sobre iSIMILAR | Domande frequenti su iSIMILAR |
| Intro | Straight answers, including what the app can't do. | Respuestas directas, también sobre lo que la app no hace. | Risposte dirette, anche su quello che l'app non fa. |

### 4.2 Preguntas y respuestas — EN

**What is iSIMILAR?**
iSIMILAR is a private visual search app for your phone's gallery, on iPhone and Android. You pick a photo or take one with the camera, and it finds the photos in your gallery that look like it. It runs entirely on the phone, without internet. From the results you can search again, move photos to an album or delete them in bulk.

**Do my photos leave my phone?**
No. Your photos and their thumbnails never leave the phone, and the visual fingerprints iSIMILAR uses to compare them are computed and stored on the device. iSIMILAR has no servers of its own.

**What data does the app collect?** [LT]
Technical data on purchases, usage and errors, never photos or gallery content. Purchases are handled by RevenueCat and error reports by Firebase (Google). This data is linked to a pseudonymous identifier, not to your name, and it isn't used for advertising or to track you across other apps. Full details are in the Privacy Policy.

**Does it work without internet?**
Yes. Scanning, searching (from a photo or the camera) and acting on the results work offline, even in airplane mode. You need a connection to download the app and to buy or restore PRO.

**Is iSIMILAR a duplicate photo cleaner?**
No. It doesn't look for exact duplicates: it finds photos that look alike, such as the same kind of object, scene or document. If you only want to remove identical copies, iOS and Google already offer free duplicate cleanup.

**Can I search by text or words?**
Not for now. You always search from an image: a photo from your gallery or one taken with the camera. You can't type "beach 2019", and you can't search by date, location or client.

**Is it like Google Lens?**
No. iSIMILAR doesn't identify objects by name, doesn't recognize faces or people and doesn't search the internet. It only compares your photo with the photos already on your phone.

**How accurate is it?**
It gets it right about 80% of the time. It works best with photos taken in similar conditions: same angle, same light, same background. Review the results before deleting.

**Does it mix up documents with other photos?**
Sometimes. Documents and phone screens get mixed up in about 1 in 5 cases. If you search from a document, expect some screens among the results, and the other way around.

**Can it find one specific photo?**
Not reliably. It groups by visual similarity, by category: a photo of a circuit board returns circuit boards in general, not one specific client's board. It's a quick way to find and review, not a way to locate an exact photo.

**Does it organize my photos automatically?**
No. You always choose the base photo and confirm every action. Nothing is moved or deleted without your confirmation.

**What's free and what's PRO?**
Searching is free. Batch actions are PRO. Free: gallery scan, unlimited searches from your saved photos, 5 camera searches and deleting photos one at a time. PRO: unlimited camera searches and batch actions, such as deleting or moving hundreds of photos at once. There are no free batch actions.

**How much does PRO cost?**
$11.99 a year in the US and €12 a year in the eurozone. In other countries, the App Store or Google Play sets the local price and shows it before you pay. It's an annual subscription with a 7-day free trial.

**How does the free trial work?** [LT]
You get 7 days of PRO. If you don't cancel before the trial ends, the annual subscription is charged. You can cancel in your App Store or Google Play subscription settings.

**Do I need an account?**
No. There's no sign-up, email or password.

**How long does the first scan take?**
On an iPhone 13 with 15,000 photos, 2.5 to 3 minutes. We haven't measured a mid-range Android phone yet. The scan runs once; after that, only new photos are processed.

**How much space does it use?**
About 3.8 KB per photo, around 38 MB for 10,000 photos. The app stores a small visual fingerprint of each photo, not copies.

**Does it work on iPhone and Android?**
Yes, on both. On iPhone you can also remove a photo from an album without deleting it and delete albums from the app.

**Does it sync between devices?**
No. Each phone keeps its own index; there's no sync or cloud backup.

**Who is it for?**
People who photograph the same kind of thing again and again: repair technicians and trades, people with galleries full of WhatsApp images, and anyone who keeps photographing products, clothes or receipts with the same layout.

### 4.3 Preguntas y respuestas — ES

**¿Qué es iSIMILAR?**
iSIMILAR es una app de búsqueda visual privada para la galería del teléfono, en iPhone y Android. Eliges una foto o haces una con la cámara, y encuentra en tu galería las fotos que se le parecen. Funciona por completo dentro del teléfono, sin internet. Desde los resultados puedes buscar de nuevo, mover fotos a un álbum o borrarlas en lote.

**¿Mis fotos salen del teléfono?**
No. Tus fotos y sus miniaturas nunca salen del teléfono, y las huellas visuales que iSIMILAR usa para compararlas se calculan y se guardan en el dispositivo. iSIMILAR no tiene servidores propios.

**¿Qué datos recoge la app?** [LT]
Datos técnicos de compras, uso y errores, sin fotos ni contenido de la galería. Las compras las gestiona RevenueCat y los informes de errores, Firebase (Google). Estos datos van asociados a un identificador seudónimo, no a tu nombre, y no se usan para publicidad ni para seguirte en otras apps. Los detalles, en la Política de privacidad.

**¿Funciona sin internet?**
Sí. El escaneo, la búsqueda (desde una foto o con la cámara) y las acciones sobre los resultados funcionan sin conexión, también en modo avión. Necesitas conexión para descargar la app y para comprar o restaurar PRO.

**¿iSIMILAR es un limpiador de fotos duplicadas?**
No. No busca duplicados exactos: encuentra fotos que se parecen, como el mismo tipo de objeto, escena o documento. Si solo quieres eliminar copias idénticas, iOS y Google ya ofrecen limpieza de duplicados gratis.

**¿Puedo buscar por texto o por palabras?**
Por ahora, no. Siempre se busca desde una imagen: una foto de tu galería o una hecha con la cámara. No puedes escribir "playa 2019" ni buscar por fecha, ubicación o cliente.

**¿Es como Google Lens?**
No. iSIMILAR no identifica objetos por su nombre, no reconoce caras ni personas y no busca en internet. Solo compara tu foto con las fotos que ya tienes en el teléfono.

**¿Cuánto acierta?**
Acierta en torno al 80% de las veces. Funciona mejor con fotos hechas en condiciones parecidas: mismo ángulo, misma luz, mismo fondo. Revisa los resultados antes de borrar.

**¿Confunde documentos con otras fotos?**
A veces. Confunde documentos con pantallas de teléfono en uno de cada cinco casos, aproximadamente. Si buscas desde un documento, es normal que aparezca alguna pantalla entre los resultados, y al revés.

**¿Encuentra una foto concreta?**
No de forma fiable. Agrupa por parecido visual, por categoría: la foto de una placa devuelve placas en general, no la placa concreta de un cliente. Sirve para encontrar rápido y revisar, no para localizar una foto exacta.

**¿Organiza mis fotos automáticamente?**
No. Tú eliges siempre la foto base y confirmas cada acción. Nada se mueve ni se borra sin tu confirmación.

**¿Qué es gratis y qué es PRO?**
Buscar es gratis. Ordenar en lote, con PRO. Gratis: escaneo de la galería, búsquedas ilimitadas desde tus fotos guardadas, 5 búsquedas con la cámara y borrado de una en una. PRO: búsquedas con cámara ilimitadas y acciones en lote, como borrar o mover cientos de fotos de una vez. No hay acciones en lote gratuitas.

**¿Cuánto cuesta PRO?**
12 € al año en la zona euro y 11,99 USD al año en EE. UU. En otros países, la App Store o Google Play fijan el precio local y lo muestran antes de pagar. Es una suscripción anual con 7 días de prueba gratis.

**¿Cómo funciona la prueba gratis?** [LT]
Tienes 7 días de PRO. Si no cancelas antes de que termine la prueba, se cobra la suscripción anual. Puedes cancelarla en los ajustes de suscripciones de la App Store o de Google Play.

**¿Necesito una cuenta?**
No. No hay registro, ni correo, ni contraseña.

**¿Cuánto tarda el primer escaneo?**
En un iPhone 13 con 15.000 fotos, entre 2,5 y 3 minutos. En un Android de gama media todavía no lo hemos medido. El escaneo se hace una vez; después solo se procesan las fotos nuevas.

**¿Cuánto espacio ocupa?**
Unos 3,8 KB por foto, unos 38 MB por cada 10.000 fotos. La app guarda una pequeña huella visual de cada foto, no copias.

**¿Funciona en iPhone y en Android?**
Sí, en los dos. En iPhone, además, puedes quitar una foto de un álbum sin borrarla y borrar álbumes desde la app.

**¿Sincroniza entre dispositivos?**
No. Cada teléfono tiene su propio índice; no hay sincronización ni copia en la nube.

**¿Para quién es?**
Para quien fotografía una y otra vez el mismo tipo de cosa: técnicos de reparación y oficios, personas con la galería llena de imágenes de WhatsApp y quien fotografía a menudo productos, ropa o recibos con el mismo formato.

### 4.4 Domande e risposte — IT

**Che cos'è iSIMILAR?**
iSIMILAR è un'app di ricerca visiva privata per la galleria del telefono, su iPhone e Android. Scegli una foto o ne scatti una con la fotocamera, e trova nella galleria le foto simili. Funziona interamente sul telefono, senza internet. Dai risultati puoi cercare di nuovo, spostare le foto in un album o eliminarle in blocco.

**Le mie foto escono dal telefono?**
No. Le tue foto e le loro miniature non lasciano mai il telefono, e le impronte visive che iSIMILAR usa per confrontarle vengono calcolate e salvate sul dispositivo. iSIMILAR non ha server propri.

**Quali dati raccoglie l'app?** [LT]
Dati tecnici su acquisti, utilizzo ed errori, mai foto o contenuti della galleria. Gli acquisti sono gestiti da RevenueCat e le segnalazioni di errore da Firebase (Google). Questi dati sono associati a un identificativo pseudonimo, non al tuo nome, e non vengono usati per pubblicità né per tracciarti in altre app. Tutti i dettagli sono nell'Informativa sulla privacy.

**Funziona senza internet?**
Sì. Scansione, ricerca (da una foto o con la fotocamera) e azioni sui risultati funzionano offline, anche in modalità aereo. La connessione serve per scaricare l'app e per acquistare o ripristinare PRO.

**iSIMILAR è un'app per eliminare le foto doppie?**
No. Non cerca i duplicati esatti: trova foto che si somigliano, come lo stesso tipo di oggetto, scena o documento. Se vuoi solo eliminare le copie identiche, iOS e Google offrono già la pulizia dei duplicati gratis.

**Posso cercare con un testo o con delle parole?**
Per ora no. Si cerca sempre partendo da un'immagine: una foto della galleria o una scattata con la fotocamera. Non puoi scrivere "spiaggia 2019" né cercare per data, luogo o cliente.

**È come Google Lens?**
No. iSIMILAR non riconosce gli oggetti per nome, non riconosce volti o persone e non cerca su internet. Confronta solo la tua foto con quelle che hai già sul telefono.

**Quanto è precisa?**
Ci azzecca circa 8 volte su 10. Funziona meglio con foto scattate in condizioni simili: stessa angolazione, stessa luce, stesso sfondo. Controlla i risultati prima di eliminare.

**Confonde i documenti con altre foto?**
A volte. In circa un caso su cinque confonde documenti e schermi di telefono. Se cerchi partendo da un documento, è normale trovare qualche schermo tra i risultati, e viceversa.

**Trova una foto precisa?**
Non in modo affidabile. Raggruppa per somiglianza visiva, per categoria: la foto di una scheda elettronica restituisce schede in generale, non quella di un cliente preciso. Serve per trovare in fretta e controllare, non per individuare una foto esatta.

**Organizza le foto in automatico?**
No. Scegli sempre tu la foto di partenza e confermi ogni azione. Niente viene spostato o eliminato senza la tua conferma.

**Cosa è gratis e cosa è PRO?**
Cercare è gratis. Per riordinare in blocco c'è PRO. Gratis: scansione della galleria, ricerche illimitate dalle foto salvate, 5 ricerche con la fotocamera ed eliminazione di una foto alla volta. PRO: ricerche con la fotocamera illimitate e azioni in blocco, come eliminare o spostare centinaia di foto in una volta. Non ci sono azioni in blocco gratuite.

**Quanto costa PRO?**
12 € all'anno nell'area euro e 11,99 USD all'anno negli Stati Uniti. Negli altri paesi il prezzo locale lo stabiliscono l'App Store o Google Play e lo vedi prima di pagare. È un abbonamento annuale con 7 giorni di prova gratuita.

**Come funziona la prova gratuita?** [LT]
Hai 7 giorni di PRO. Se non disdici prima della fine della prova, viene addebitato l'abbonamento annuale. Puoi disdirlo dalle impostazioni abbonamenti dell'App Store o di Google Play.

**Serve un account?**
No. Niente registrazione, email o password.

**Quanto dura la prima scansione?**
Su un iPhone 13 con 15.000 foto, da 2,5 a 3 minuti. Su un Android di fascia media non l'abbiamo ancora misurata. La scansione si fa una volta; dopo vengono elaborate solo le foto nuove.

**Quanto spazio occupa?**
Circa 3,8 KB per foto, circa 38 MB ogni 10.000 foto. L'app salva una piccola impronta visiva di ogni foto, non delle copie.

**Funziona su iPhone e Android?**
Sì, su entrambi. Su iPhone puoi anche togliere una foto da un album senza eliminarla ed eliminare album dall'app.

**Sincronizza tra dispositivi?**
No. Ogni telefono ha il suo indice; non c'è sincronizzazione né backup nel cloud.

**Per chi è?**
Per chi fotografa sempre lo stesso tipo di cose: tecnici e artigiani, chi ha la galleria piena di immagini di WhatsApp e chi fotografa spesso prodotti, vestiti o scontrini con lo stesso formato.

---

## 5. Textos actuales que se eliminan o cambian

Líneas de `solopila_landingPAGE/web/i18n.js`. Cada clave tiene tres líneas: EN · ES (+96) · IT (+192).
Las que no están en `i18n.js` llevan la línea de `index.html`.

| Clave / elemento | Líneas EN · ES · IT | Texto actual (EN) | Acción | Por qué (regla) |
|---|---|---|---|---|
| `meta.title` | 4 · 100 · 196 | iSIMILAR — Similar image search | Cambia | Sin el verbo que se busca ("find") ni "offline"; nuevo title por página |
| `meta.description` | 5 · 101 · 197 | …in under 0.5s. 100% offline… | Cambia | "0,5 s" prohibido (definición técnica, Rendimiento: se dice "menos de un segundo") |
| `meta.ogTitle` | 6 · 102 · 198 | Your phone searches by words. iSIMILAR searches by what your eyes see. | Cambia | Comparación implícita no verificable: Apple Fotos también busca dentro del teléfono (brief, tabla) |
| `meta.ogDescription` | 7 · 103 · 199 | The first visual similar-image search engine… invoices… 0.5s | Cambia | "El primero" (existe Queryable), "facturas" (no busca por texto), "0,5 s" |
| `meta.twTitle` / `meta.twDescription` | 9-10 · 105-106 · 201-202 | 100% Offline Photo Search / …in under 0.5s. Total privacy… | Cambia | "0,5 s"; "Total privacy" choca con "no se puede decir: cero recopilación" |
| `hero.badge` | 12 · 108 · 204 | 🔒 100% Offline • No Cloud • Local AI Search | Cambia | Se simplifica; "Sin cuenta" aporta más que "IA local" |
| `hero.h1a` + `hero.h1b` | 13-14 · 109-110 · 205-206 | Your phone searches by words. iSIMILAR searches by what your eyes see. | Cambia | Misma comparación implícita; el nuevo H1 usa el concepto del brief ("mirando, no escribiendo") y la búsqueda "find similar photos" |
| `hero.lead` | 15 · 111 · 207 | The first intelligent… in under 0.5 seconds… no paying the cloud | Cambia | "El primero", "0,5 s", "clean up" (atrae a quien busca limpiador), argumento de la nube débil (guía, Acumulador) |
| `hero.trust` | 18 · 114 · 210 | Free forever • No account required • Works in Airplane Mode | Cambia | "Gratis para siempre" a secas → "Búsqueda gratis para siempre" (brief, tabla) |
| Franja de datos | `index.html` 136 + claves `stats.*` 20-23 · 116-119 · 212-215 | < 0.5s · ~23 MB · 0 cloud servers · 0 accounts | Cambia | "0,5 s" y "23 MB" prohibidos (definición técnica: 38 MB/10.000 fotos); "0 servidores" engaña: RevenueCat y Firebase sí reciben datos |
| `pain.h2`, `pain.c1t` | 24, 26 · 120, 122 · 216, 218 | The "cross-contamination" of your gallery | Cambia | Jerga; el dolor se dice en palabras del usuario (guía, Posicionamiento) |
| `pain.c2t`/`c2p` | 28-29 · 124-125 · 220-221 | The Accidental Swipe Danger / mini heart attack… | Cambia (se conserva la idea) | Idea válida (brief, ideas de vídeo); tono exagerado |
| `pain.c3t`/`c3p` | 30-31 · 126-127 · 222-223 | The Cloud Blackmail / Paying $3 or $10 a month… | Elimina | Argumento de iCloud débil (guía) y cifras sin fuente; se sustituye por memes/capturas (segmento 2) |
| `steps.h2a` | 32 · 128 · 224 | The magic in | Elimina | "Magia" prohibida (brief, Tono) |
| `steps.sub` | 34 · 130 · 226 | No tags. No keywords. Just vision. | Elimina | Vacío de contenido; se explica qué compara |
| `steps.c2t`/`c2p` | 36-37 · 132-133 · 228-229 | Visual DNA Detection / Neural Engine… in 0.5 seconds | Cambia | "0,5 s"; "Neural Engine" es de Apple y falso en Android; "ADN visual" es exageración |
| `steps.c3p` | 39 · 135 · 231 | …secure album… free up gigabytes in one tap | Cambia | El álbum no es "seguro" (es un álbum normal del sistema); "liberar gigas" sin datos (brief, tabla) |
| `cmp.*` (tabla comparativa entera) | 41-58 · 137-154 · 233-250 | iSIMILAR versus Google Photos and Apple Photos… WiFi required… external servers… < 0.5 seconds | Elimina | Comparación falsa (Apple Fotos busca sin conexión) y prohibida (brief; decisión, opción A). Se rehace solo con datos comprobables y fechados (decisión, "Para más adelante") |
| `aud.c1p` | 64 · 160 · 256 | …isolate work evidence… | Cambia | "Evidencias" sugiere uso pericial (perfil excluido en el brief); se usa "Separa tus fotos de trabajo en minutos" |
| `aud.c2t`/`c2p` | 65-66 · 161-162 · 257-258 | Freelancers and Administration / Find all invoices, tickets and receipts in seconds | Elimina | "Todas tus facturas" prohibido (brief, tabla) |
| `aud.c3t`/`c3p` | 67-68 · 163-164 · 259-260 | Digital Hoarders / more than 10,000 photos… | Cambia | Se reorienta a "galería llena de WhatsApp" (segmento 2 del brief) |
| `price.sub` | 71 · 167 · 263 | Real freemium. Start free… | Cambia | Se sustituye por "Buscar es gratis. Ordenar en lote, con PRO." (brief, Precio) |
| Precio | `index.html` 171 | $12.99 / year | Cambia | Precio real: 11,99 USD / 12 € (brief, Precio) |
| `price.f1` | 75 · 171 · 267 | Unlimited magical camera search | Cambia | "Mágica" prohibido |
| `price.f3` | 77 · 173 · 269 | Average savings of 15 GB… | Elimina | Sin datos (brief, tabla) |
| `price.freeText` | 81 · 177 · 273 | unlimited gallery searches, full local scanning and manual one-by-one deletion | Cambia | Falta "5 búsquedas con cámara" (brief, Precio) |
| `price.note` | 79 · 175 · 271 | The final price may vary… | Cambia | Se añade cómo funciona la renovación tras la prueba [LT] |
| `faq.a1` | 85 · 181 · 277 | iSIMILAR has no cloud servers… | Cambia | Cierto para fotos, pero hay que decir qué datos sí salen (brief, tabla; guía, Prioridades 1) |
| `faq.a2` | 87 · 183 · 279 | It is much more powerful… | Cambia | Superlativo; "fotos en ráfaga" y "misma placa" sugieren instancia, no categoría |
| `faq.a3` | 89 · 185 · 281 | …only ~23 MB… | Cambia | Dato incorrecto: unos 38 MB por 10.000 fotos (definición técnica) |
| `faq.a4` | 91 · 187 · 283 | Zero emails, zero passwords, zero personal data collection | Cambia | "Cero recopilación de datos" prohibido (brief, tabla) |
| `final.h2a`/`h2b` | 92-93 · 188-189 · 284-285 | Kill the chaos of your gallery today. | Cambia | Tono agresivo; sin pilar |
| `final.sub` | 94 · 190 · 286 | Download it free. No account. No cloud. | Cambia | "Gratis" a secas (guía, Reglas de mensaje) |
| `footer.privacy` | 96 · 192 · 288 | Privacy Policy (100% local processing) | Cambia | "100% local" es falso para compras y errores; enlaces a "#" (`index.html` 191) |
| Detección de idioma | `i18n.js` 293-298, 309 | Cambia el idioma en la misma URL según el navegador | Se sustituye | Decisión: una URL por idioma; detección solo en `/` y solo la primera vez |
| Enlace App Store | `index.html` 198 | `apps.apple.com/us/app/...` | Cambia | Enlace neutro con token de campaña (sección 7) |

Se reaprovecha (con retoques): `nav.download`, `store.*`, `steps.c1t`/`c1p` (idea), `aud.c1t` (idea),
`price.pill` (7 días de prueba), `price.cta`, `faq.q1`, `faq.q2`, `faq.q4` (preguntas, no respuestas), `final.qr`.

---

## 6. Palabras de búsqueda propuestas

**Qué verifiqué y qué no.** No tengo acceso a datos de volumen (Apple Search Ads, Google Keyword
Planner, Search Console de isimilar.app). **No puedo confirmar el volumen de ninguna de estas
búsquedas.** Lo único que comprobé hoy (2026-10-21) con búsquedas web es que la expresión aparece
en contenidos reales (artículos, foros, fichas de la competencia), lo que indica uso pero no cantidad.

Leyenda: **U** = uso comprobado en contenido real hoy (sin volumen) · **G** = la guía dice que es
búsqueda real, sin dato a la vista · **H** = hipótesis.

### EN
| Búsqueda | Página | Estado | Nota |
|---|---|---|---|
| find similar photos (on iPhone) | Inicio | U | Artículo de MacPaw "find similar photos on iPhone" |
| similar photo finder | Inicio | H | Propuesta de título de tienda en la guía; mezcla intención "limpiador" |
| search photos by image | Cómo funciona | H | |
| offline photo search / private photo search | Inicio, FAQ | H | El subtítulo actual de la tienda ("Private Visual Search Engine") usa palabras que "casi nadie busca" según la guía |
| visual search app for camera roll | Cómo funciona | H | |
| separate work photos from personal photos | Inicio (perfil 1) | H | Búsqueda de alta intención para el segmento 1; sin volumen comprobado |
| delete similar screenshots / memes in bulk | Inicio (perfil 2) | H | Riesgo: atrae a quien busca limpiador |
| app like Google Lens for my gallery / offline | FAQ | H | Posible búsqueda en asistentes de IA |

### ES
| Búsqueda | Página | Estado | Nota |
|---|---|---|---|
| buscar fotos parecidas | Inicio | H | Español neutro; "parecidas" vs "similares" sin dato |
| fotos similares (iSIMILAR: Fotos Similares) | Inicio | G | La guía lo propone como título de tienda y dice que el subtítulo ES ya usa búsquedas reales |
| app para buscar fotos parecidas sin internet | FAQ | U | Hay contenido que responde a esa búsqueda (artículos de Tenorshare, Google Gallery Go) |
| buscar por imagen en la galería | Cómo funciona | H | Riesgo: "buscar por imagen" suele ser búsqueda inversa en internet |
| separar fotos de trabajo y personales | Inicio (perfil 1) | H | La guía la usa como ejemplo de pregunta a la IA |
| borrar memes de WhatsApp | Inicio (perfil 2) | H | |
| mover muchas fotos a un álbum | Cómo funciona | H | |

### IT
| Búsqueda | Página | Estado | Nota |
|---|---|---|---|
| trovare foto simili | Inicio | U | Artículos de iPhoneItalia y Macitynet sobre "foto simili" |
| foto simili iPhone | Inicio | U | Mismo contenido; dominado por limpiadores de duplicados |
| ricerca per immagine nella galleria | Cómo funciona | U | Hilo de la comunidad Samsung: "Ricercare nella galleria con una immagine per immagini simili" |
| app foto simili (iSIMILAR: Foto Simili) | Inicio | G | Propuesta de título de tienda en la guía |
| cercare foto con un'immagine senza internet | FAQ | H | |
| separare foto di lavoro e personali | Inicio (perfil 1) | H | |
| eliminare meme WhatsApp | Inicio (perfil 2) | H | |

**Cómo convertir las hipótesis en datos (0 €):**
1. Apple Search Ads (cuenta gratis, sin gastar): el planificador da una "popularidad" por palabra
   en EE. UU. y otros países. Revisar todas las EN antes del montaje de la Fase 2.
2. Google Search Console, a las 4 semanas de publicar: consultas reales con impresiones por página.
3. Prueba mensual en ChatGPT, Perplexity, Gemini y Copilot con 3 preguntas por idioma (guía, Canales).

**Riesgo común:** "similar photos" y "foto simili" están dominadas por limpiadores de duplicados.
Atraen visitas que la FAQ desmiente ("no es un limpiador"). Por eso el texto apunta a intención
de búsqueda visual ("find", "search by image", "separate work photos") y no a "clean" o "duplicate".

---

## 7. Hipótesis, medición y decisión

| # | Hipótesis | Dato y fuente | Línea base | Cuándo se decide |
|---|---|---|---|---|
| 1 | Una URL por idioma con texto en el HTML hace que Google indexe las tres versiones y reciba búsquedas en ES e IT | Páginas indexadas e impresiones por idioma · Google Search Console y Bing Webmaster Tools | 0 (hoy una sola versión indexable) | 4 semanas tras publicar |
| 2 | La web pasa a traer descargas medibles | Descargas con token `ct` por página e idioma (`ct=web_en_home`, `web_es_faq`…) · App Store Connect, Campañas; `referrer=utm_…` · Google Play Console | Webs: "casi nada" (guía, App Store) | 8 semanas tras publicar |
| 3 | La FAQ hace que los asistentes de IA describan bien la privacidad y el modelo (sin "datos para publicidad") | Registro mensual: 3 preguntas × 3 idiomas × 4 asistentes; ¿aparece iSIMILAR?, ¿la describen bien? · hoja propia | Prueba de octubre en la guía (ChatGPT con el error de privacidad; Gemini no la recomienda) | Primera repetición 4 semanas tras publicar; decisión a las 8 |
| 4 | Más descargas desde ChatGPT tras la web nueva | Referencias de apps "ChatGPT" · App Store Connect | 51 descargas (finales de agosto–13 oct) | 8 semanas tras publicar |
| 5 | Que lleguen pagos de la web | Ingresos por campaña `ct` · App Store Connect (si lo muestra por campaña; no puedo confirmar que RevenueCat lo atribuya) | 0 atribuibles | 8 semanas tras publicar |

Criterio de éxito propuesto (orientativo, a fijar por Anibal antes de publicar): la web aparece
como origen con al menos 1 descarga por semana y los asistentes dejan de atribuir publicidad a la app.
Si a las 8 semanas Search Console no muestra impresiones en ES o IT, se revisan las palabras de la sección 6
antes de escribir las páginas de casos de uso (Fase 4).

---

## 8. Revisión con `tono-de-marca`

| Frase | Problema | Regla | Versión entregada |
|---|---|---|---|
| "Free search, forever" / "Búsqueda gratis para siempre" | Puede leerse como "todo gratis" | Brief: se permite "Búsqueda gratis para siempre" | Se mantiene, y la sección de precio aclara el límite de cámara |
| "Buscar es gratis" | La cámara solo tiene 5 búsquedas gratis | Brief, Precio: frase obligatoria | Se mantiene y siempre va seguida de la lista Gratis con "5 búsquedas con la cámara" |
| "Your photos never leave your phone" | Correcto solo para fotos | Brief: permitido; guía: no decir "Nada sale de tu teléfono" | Nunca se usa "nada sale"; se usa "sin subir tus fotos" |
| "Under 1 second per search" | Sin medición formal | Definición técnica: se dice "menos de un segundo" hasta medir | Permitido |
| "about 80% of the time" / "8 volte su 10" | Ver contradicción 3 | Brief, Qué es | Se mantiene la cifra del brief |
| "No account" | No figura en el brief | Comprobado en la ficha de App Store: "no accounts needed" | Permitido |
| "iOS and Google already offer free duplicate cleanup" | Mención a terceros | Guía, Acumulador: lo afirma | Se mantiene sin comparar calidad; Anibal decide si prefiere quitarlo |
| "isn't used for advertising or to track you" | Afirmación legal | Definición técnica: etiqueta "sin rastreo ni publicidad" | Marcada [LT] |

Pilares: cada sección se apoya en Encuentra (hero, cómo funciona), Ordena (perfiles, precio) o Privado
(franja, FAQ). Sin "magia", "el primero", "exacta", "0,5 s", "50 ms", "15 GB", "anónimo", "100% gratis",
"5 free actions" ni comparaciones con Google Fotos o Apple Fotos.

**Veredicto: apto con cambios** — pendiente de las respuestas [LT] de legal-tiendas, de las
contradicciones de la sección 9 y de comprobar la imagen del hero.

---

## 9. Contradicciones detectadas

⚠️ Contradicción detectada
- Documento: `docs/guia-estrategica.md` · "Qué es realmente iSIMILAR", tabla (línea 217) dice: no se puede decir "Nada sale de tu teléfono", porque Crashlytics y RevenueCat se comunican con servidores.
- Fuente: `docs/brief-marketing.md` · frase central (línea 50) dice "sin internet y sin subir nada", y la captura 5 (línea 135) dice "100% offline. Nothing uploaded".
- Impacto: la web, la ficha y los vídeos pueden repetir una promesa que la guía prohíbe. En este borrador uso "sin subir tus fotos" para cumplir ambos.
- Opciones: A) ajustar la fuente al documento · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada
- Documento: `docs/brief-marketing.md` · "Lo que se puede y no se puede decir" (línea 66) prohíbe "encuentra cualquier foto"; `docs/definicion-tecnica.md` · Arquitectura (línea 17) limita a 250 resultados y Límites (línea 37) da un 80%.
- Fuente: `docs/brief-marketing.md` · captura 1 (línea 131): "Find every photo that looks like this".
- Impacto: "every" promete exhaustividad. No lo uso en la web; afecta a la captura 1 de la tienda.
- Opciones: A) ajustar la fuente al documento · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada
- Documento: `docs/definicion-tecnica.md` · Límites (línea 37) dice: "Precisión en torno al 80% (mAP de 0,79 medido sobre 917 imágenes)".
- Fuente: `docs/brief-marketing.md` · Qué es (línea 13) dice: "Acierta en torno al 80% de las veces".
- Impacto: un mAP de 0,79 no es lo mismo que "acertar 8 de cada 10 veces" (mide la calidad del orden de los resultados). En la FAQ, una cifra que la IA va a citar debe ser defendible. Uso la frase del brief porque es la que manda sobre lo que se dice.
- Opciones: A) ajustar la fuente al documento · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada
- Documento: `docs/brief-marketing.md` · Precio (línea 77): el plan gratis incluye 5 búsquedas con cámara.
- Fuente: `docs/guia-estrategica.md` · La web isimilar.app, tabla (línea 175) propone "Búsqueda desde la galería gratis; cámara y acciones en lote con PRO".
- Impacto: menor; si se copia la propuesta de la guía, la web diría que la cámara es solo de PRO. Uso el brief.
- Opciones: A) ajustar la fuente al documento · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada
- Documento: `docs/brief-marketing.md` · Para quién (línea 46): los sanitarios no se usan como mensaje principal.
- Fuente: ficha pública de la App Store (consultada el 2026-10-21): la descripción se dirige a "doctors" y localiza radiografías (también señalado en la guía, línea 166).
- Impacto: fuera del alcance de la web, pero los asistentes de IA leen la ficha y la web; si no coinciden, repiten la ficha.
- Opciones: A) ajustar la fuente al documento · B) Anibal revisa el documento
- Esperando decisión.

---

## 10. Dudas abiertas para Anibal

1. **"Pantallas de móvil"**: ¿son capturas de pantalla o fotos de pantallas físicas (las que hace un técnico)? He escrito "pantallas de teléfono / phone screens / schermi di telefono" para no elegir. Si son capturas, cambia el texto y el ejemplo de WhatsApp.
2. **Compartir en lote**: ¿compartir varias fotos a la vez es PRO o gratis? La definición técnica no lo dice. No lo he puesto en la lista de PRO ni en la de gratis.
3. **¿Funciona todo sin conexión desde la primera apertura?** (¿RevenueCat necesita red para arrancar?). He escrito que hace falta conexión para descargar y para comprar o restaurar, nada más.
4. **Prueba de 7 días**: la guía propone cambiarla (límite en lote o pago único). Si cambia, hay que tocar precio y FAQ en 3 idiomas; conviene que en Astro el precio sea un único componente.
5. **URLs de privacidad y términos en ES e IT**: ¿una sola `/privacy` multilingüe o `/es/privacidad` e `/it/privacy`? Lo decide legal-tiendas; el pie está preparado para cambiar.
6. **Enlaces del pie mientras no existan `/privacy` y `/terms`**: ¿se publican a la vez o se apunta temporalmente a Notion?
7. **Imagen del hero y `og:image`**: ¿qué muestran hoy? No las he visto; si llevan textos antiguos ("5 free actions", 12,99 USD), hay que rehacerlas.
8. **Mención a duplicados de iOS y Google** en la FAQ: es honesta y la recoge la guía, pero manda tráfico a la competencia gratuita. ¿Se mantiene?


### Respuestas de Anibal (2026-10-23)

1. Son **fotos de pantallas físicas** de celulares (en su trabajo fotografía pantallas de clientes con emails y contraseñas para recordarlas o gestionarlas). Mantener "pantallas de teléfono / phone screens / schermi di telefono" y ajustar el ejemplo si sugiere capturas.
2. Compartir en lote **no existe todavía**: llega en la versión que se está terminando y será **PRO** (todas las acciones en lote son PRO). Incluirlo en la lista de PRO.
3. **Funciona en modo avión desde la primera apertura.**
6. El pie enlaza a `/privacy` y `/terms` en la web (no a Notion), con el texto de `2026-10-22-legal-politicas-v3.md`. Se publican ya, dentro de Astro.
8. Se mantiene. Texto propuesto por Anibal (ES):

> **¿Es un limpiador de duplicados?**
> No. Para copias exactas, tu teléfono probablemente ya tiene una herramienta gratuita: en iPhone, el álbum "Duplicados" de Fotos; en Android, Files by Google o la galería de algunos fabricantes. iSIMILAR hace otra cosa: encuentra fotos que se parecen aunque no sean iguales, como distintos ángulos de la misma placa, productos del mismo estante o capturas con el mismo diseño, y te deja moverlas o borrarlas en lote.

Condiciones: (a) comprobar con una búsqueda en la web que esas funciones siguen existiendo con esos nombres antes de publicar; (b) no decir nada negativo de esas herramientas.

Siguen abiertas: 4 (prueba de 7 días), 5 (URL legales por idioma) y 7 (imagen del hero y `og:image`).

---

## Fuentes consultadas hoy (2026-10-21)

- Ficha de iSIMILAR en la App Store: https://apps.apple.com/us/app/isimilar/id6738889078 (precio 11,99 USD, "no accounts needed", etiqueta de privacidad, mención a "doctors").
- MacPaw, "find similar photos on iPhone": https://macpaw.com/how-to/find-similar-photos-on-iphone
- iPhoneItalia, "Come eliminare foto doppie e simili su iPhone": https://www.iphoneitalia.com/848101/eliminare-foto-doppie-iphone
- Macitynet: https://www.macitynet.it/?p=452827
- Comunidad Samsung (IT), "Ricercare nella galleria con una immagine per immagini simili": https://eu.community.samsung.com/t5/galaxy-s24-series/ricercare-nella-galleria-con-una-immagine-per-immagini-simili/td-p/10968425 (solo título; la página devolvió 403)
- Tenorshare 4DDiG (ES): https://4ddig.tenorshare.com/es/eliminar-duplicados/find-similar-images.html
- Android Central, "Google Photos 'More like this' button": https://www.androidcentral.com/google-photos-more-like-this-button (solo titular; confirma que Google Fotos tiene una función de imágenes parecidas: otra razón para no compararse sin datos fechados)
