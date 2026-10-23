# Web isimilar.app (Astro) · Correcciones pedidas por Anibal

Borrador de `growth` · 2026-10-23 · Estado: **pendiente de decisión de Anibal**
Base: `solopila_landingPAGE/astro/src/i18n/en.json`, `es.json`, `it.json` (versión publicada hoy).
No se tocan `src/legal/` ni `docs/`. Aquí no se edita la web: los cambios se aplican en una sesión abierta en `solopila_landingPAGE/`.

Formato: **clave JSON · idioma · antes → ahora**. Las rutas usan índices desde 0, como el código (`faq.items[0]` = "¿Qué es iSIMILAR?").

**Orden de aplicación:** el punto 6 inserta una pregunta nueva en `faq.items[3]`. Todas las rutas de este documento se refieren al JSON **actual**; aplica el punto 6 el último (o suma 1 a cualquier índice `faq.items[n]` con n ≥ 3 si lo aplicas antes).

Límites usados (los mismos del borrador del 21): `title` ≤ 60 caracteres, `description` ≤ 155. Recuentos hechos con script, espacios incluidos.

---

## 1. Definición: "buscador privado de imágenes similares"

### Valoración

A favor de Anibal:
- "Buscador visual privado" dice cómo busca, no qué encuentra. "De imágenes similares" dice el resultado y repite la palabra del nombre (iSIMILAR = similar). Para un asistente de IA, "X es un [categoría] de [objeto]" es la frase que mejor se extrae y se cita.
- "Imágenes similares / similar images / immagini simili" es lo que escribe la gente. No puedo confirmar volúmenes de búsqueda (no tengo acceso a datos de palabras clave); es criterio cualitativo.

En contra, y cómo lo resuelvo:
- **Intención de búsqueda equivocada.** Quien busca "buscar imágenes similares" casi siempre quiere búsqueda inversa en internet (Google Lens, Google Imágenes, TinEye). iSIMILAR es justo lo contrario (brief: "No es Google Lens"). Por eso la fórmula va siempre pegada a "privado" y a "galería del teléfono", y nunca sola en un título. Los títulos siguen con "fotos parecidas / similar photos / foto simili", que ya indica "tus fotos".
- **"Visual" sobra.** "Buscador visual de imágenes similares" repite la idea (visual + imágenes). Propongo quitar "visual" y conservar "privado", que es el pilar diferencial. Si Anibal quiere "visual", la alternativa es "buscador visual privado de imágenes similares": correcta, pero larga.
- **Orden de palabras:** el adjetivo va con "buscador" ("buscador privado de imágenes similares"), no con las imágenes ("buscador de imágenes similares privadas" diría que las fotos son privadas, no la búsqueda).

Nota (no es contradicción, es divergencia de redacción): `docs/brief-marketing.md` (línea 9) define la app como "un buscador visual privado para la galería del móvil". La nueva fórmula no contradice el contenido, pero la web y el brief dejan de usar la misma frase. Para que tienda, web e IA repitan una sola definición, Anibal decide si el brief adopta la nueva (yo no lo toco).

### Cambios

**`how.intro`**
- EN · antes: iSIMILAR is a private visual search engine for your phone's gallery. You give it a photo and it shows you the ones that look like it. Everything runs on the phone, without internet.
- EN · ahora: iSIMILAR is a private search engine for similar images in your phone's gallery. You give it a photo and it shows you the ones that look like it. Everything runs on the phone, without internet.
- ES · antes: iSIMILAR es un buscador visual privado para la galería del teléfono. Le das una foto y te muestra las que se le parecen. Todo ocurre dentro del teléfono, sin internet.
- ES · ahora: iSIMILAR es un buscador privado de imágenes similares para la galería del teléfono. Le das una foto y te muestra las que se le parecen. Todo ocurre dentro del teléfono, sin internet.
- IT · antes: iSIMILAR è un motore di ricerca visiva privato per la galleria del telefono. Gli dai una foto e ti mostra quelle simili. Tutto avviene sul telefono, senza internet.
- IT · ahora: iSIMILAR è un motore di ricerca privato per immagini simili nella galleria del telefono. Gli dai una foto e ti mostra quelle che le somigliano. Tutto avviene sul telefono, senza internet.

(IT: "quelle che le somigliano" evita repetir "simili" dos veces en dos frases.)

**`faq.items[0].a`** ("¿Qué es iSIMILAR?"; la pregunta no cambia)
- EN · antes: iSIMILAR is a private visual search app for your phone's gallery, on iPhone and Android. You pick a photo or take one with the camera, and it finds the photos in your gallery that look like it. It runs entirely on the phone, without internet. From the results you can search again and, with PRO, move photos to an album, share them or delete them in bulk.
- EN · ahora: iSIMILAR is a private search engine for similar images in your phone's gallery, on iPhone and Android. You pick a photo or take one with the camera, and it finds the ones that look like it. It runs entirely on the phone, without internet. From the results you can search again and, with PRO, move photos to an album, share them or delete them in bulk.
- ES · antes: iSIMILAR es una app de búsqueda visual privada para la galería del teléfono, en iPhone y Android. Eliges una foto o haces una con la cámara, y encuentra en tu galería las fotos que se le parecen. Funciona por completo dentro del teléfono, sin internet. Desde los resultados puedes buscar de nuevo y, con PRO, mover fotos a un álbum, compartirlas o borrarlas en lote.
- ES · ahora: iSIMILAR es un buscador privado de imágenes similares para la galería del teléfono, en iPhone y Android. Eliges una foto o haces una con la cámara, y encuentra en tu galería las que se le parecen. Funciona por completo dentro del teléfono, sin internet. Desde los resultados puedes buscar de nuevo y, con PRO, mover fotos a un álbum, compartirlas o borrarlas en lote.
- IT · antes: iSIMILAR è un'app di ricerca visiva privata per la galleria del telefono, su iPhone e Android. Scegli una foto o ne scatti una con la fotocamera, e trova nella galleria le foto simili. Funziona interamente sul telefono, senza internet. Dai risultati puoi cercare di nuovo e, con PRO, spostare le foto in un album, condividerle o eliminarle in blocco.
- IT · ahora: iSIMILAR è un motore di ricerca privato per immagini simili nella galleria del telefono, su iPhone e Android. Scegli una foto o ne scatti una con la fotocamera, e trova nella galleria quelle che le somigliano. Funziona interamente sul telefono, senza internet. Dai risultati puoi cercare di nuovo e, con PRO, spostare le foto in un album, condividerle o eliminarle in blocco.

(Esta respuesta también va al JSON-LD `FAQPage`, que se genera solo desde `faq.items`.)

**`home.meta.description`** (recomendado). Motivo: `Home.astro` usa este mismo texto como `description` del JSON-LD `SoftwareApplication`, que es lo que leen buscadores e IA como definición de la app. Hoy no contiene ninguna categoría.
- EN · antes (145): Pick a photo or point your camera and iSIMILAR finds the ones that look alike in your gallery. Works offline; your photos never leave your phone.
- EN · ahora (154): iSIMILAR is a private search engine for similar images in your phone's gallery. Pick a photo or point your camera. Offline; photos never leave your phone.
- ES · antes (123): Elige una foto o apunta la cámara: iSIMILAR encuentra las que se parecen en tu galería. Sin internet y sin subir tus fotos.
- ES · ahora (154): iSIMILAR es un buscador privado de imágenes similares para la galería del teléfono. Elige una foto o apunta la cámara: sin internet y sin subir tus fotos.
- IT · antes (133): Scegli una foto o inquadra un oggetto: iSIMILAR trova in galleria le foto simili. Funziona offline: le tue foto restano sul telefono.
- IT · ahora (153): iSIMILAR è un motore di ricerca privato per immagini simili nella galleria. Scegli una foto o inquadra un oggetto: offline, le foto restano sul telefono.

Contra: pierde la frase central del brief tal cual ("Elige una foto o apunta la cámara: iSIMILAR encuentra las que se parecen…") en el fragmento de Google. La conservan el hero y `ogDescription`. Si Anibal prefiere no tocarla, el resto del punto 1 funciona igual.

**No cambian:** `home.meta.title`, `how.meta.*`, `faq.meta.*`, `ogTitle`/`ogDescription`: ya dicen "similar photos / fotos parecidas / foto simili", que es la búsqueda con intención de galería, y meter "imágenes similares" en un título atrae la búsqueda inversa de Google (ver arriba).

---

## 2. Primer escaneo en Android (Xiaomi Mi A3)

⚠️ Contradicción detectada
- Documento: `docs/definicion-tecnica.md` · Rendimiento medido dice: "Primer escaneo, Android de gama media · Sin medir" (y "Pendiente de confirmar": "Tiempo del primer escaneo en un Android de gama media").
- Fuente: petición de Anibal (2026-10-23) dice: Xiaomi Mi A3, unas 8.000 fotos, alrededor de 4-5 minutos. Los textos nuevos de abajo publican ese dato.
- Impacto: la web afirmaría un dato que el documento de referencia declara sin medir. Si un asistente de IA cruza la web con otra fuente, hay dos versiones.
- Opciones: A) ajustar la fuente al documento (la web sigue diciendo "sin medir") · B) Anibal revisa el documento y añade la medición
- Esperando decisión. Los textos están escritos para la opción B (Anibal ha dicho que actualizará el documento); publicarlos cuando el documento esté actualizado.

Preguntas para que el dato aguante (y para el documento): ¿una sola medición o varias? ¿Versión de la app y de Android? ¿Pantalla encendida y app en primer plano? ¿GPU activada? El Mi A3 (julio de 2019, Snapdragon 665) es un gama media de hace seis años: es un dato prudente, juega a favor. Escribo el modelo concreto en vez de "un Android de gama media" porque es verificable y no se discute qué es "gama media". Ojo: el modelo destilado de la hoja de ruta obliga a reescanear; el tiempo habrá que medirlo de nuevo antes de anunciarlo.

**`how.sections[0].p`**
- EN · antes: The first time you open the app, it scans your gallery once, even without a connection. On an iPhone 13 with 15,000 photos it takes 2.5 to 3 minutes; we haven't measured it yet on a mid-range Android phone. After that, it only processes new photos, and if the scan is interrupted it picks up where it left off. Your originals aren't copied or moved: the app keeps a small visual fingerprint of each photo, on the phone.
- EN · ahora: The first time you open the app, it scans your gallery once, even without a connection. On an iPhone 13 with 15,000 photos it takes 2.5 to 3 minutes; on a Xiaomi Mi A3 (a 2019 mid-range Android phone) with about 8,000 photos, around 4 to 5 minutes. After that, it only processes new photos, and if the scan is interrupted it picks up where it left off. Your originals aren't copied or moved: the app keeps a small visual fingerprint of each photo, on the phone.
- ES · antes: La primera vez que abres la app, escanea tu galería una sola vez, también sin conexión. En un iPhone 13 con 15.000 fotos tarda entre 2,5 y 3 minutos; en un Android de gama media todavía no lo hemos medido. Después solo procesa las fotos nuevas, y si el escaneo se interrumpe, sigue desde donde se quedó. Tus originales no se copian ni se mueven: la app guarda una pequeña huella visual de cada foto, dentro del teléfono.
- ES · ahora: La primera vez que abres la app, escanea tu galería una sola vez, también sin conexión. En un iPhone 13 con 15.000 fotos tarda entre 2,5 y 3 minutos; en un Xiaomi Mi A3 (Android de gama media de 2019) con unas 8.000 fotos, entre 4 y 5 minutos. Después solo procesa las fotos nuevas, y si el escaneo se interrumpe, sigue desde donde se quedó. Tus originales no se copian ni se mueven: la app guarda una pequeña huella visual de cada foto, dentro del teléfono.
- IT · antes: La prima volta che apri l'app, analizza la galleria una sola volta, anche senza connessione. Su un iPhone 13 con 15.000 foto ci vogliono da 2,5 a 3 minuti; su un Android di fascia media non l'abbiamo ancora misurato. Dopo elabora solo le foto nuove e, se la scansione si interrompe, riprende da dove si era fermata. Gli originali non vengono copiati né spostati: l'app salva sul telefono una piccola impronta visiva di ogni foto.
- IT · ahora: La prima volta che apri l'app, analizza la galleria una sola volta, anche senza connessione. Su un iPhone 13 con 15.000 foto ci vogliono da 2,5 a 3 minuti; su uno Xiaomi Mi A3 (Android di fascia media del 2019) con circa 8.000 foto, tra 4 e 5 minuti. Dopo elabora solo le foto nuove e, se la scansione si interrompe, riprende da dove si era fermata. Gli originali non vengono copiati né spostati: l'app salva sul telefono una piccola impronta visiva di ogni foto.

**`faq.items[15].a`** ("¿Cuánto tarda el primer escaneo?")
- EN · antes: On an iPhone 13 with 15,000 photos, 2.5 to 3 minutes. We haven't measured a mid-range Android phone yet. The scan runs once; after that, only new photos are processed.
- EN · ahora: On an iPhone 13 with 15,000 photos, 2.5 to 3 minutes. On a Xiaomi Mi A3 (a 2019 mid-range Android phone) with about 8,000 photos, around 4 to 5 minutes. The time depends on your phone and on how many photos you have. The scan runs once; after that, only new photos are processed.
- ES · antes: En un iPhone 13 con 15.000 fotos, entre 2,5 y 3 minutos. En un Android de gama media todavía no lo hemos medido. El escaneo se hace una vez; después solo se procesan las fotos nuevas.
- ES · ahora: En un iPhone 13 con 15.000 fotos, entre 2,5 y 3 minutos. En un Xiaomi Mi A3 (Android de gama media de 2019) con unas 8.000 fotos, entre 4 y 5 minutos. El tiempo depende de tu teléfono y de cuántas fotos tengas. El escaneo se hace una vez; después solo se procesan las fotos nuevas.
- IT · antes: Su un iPhone 13 con 15.000 foto, da 2,5 a 3 minuti. Su un Android di fascia media non l'abbiamo ancora misurata. La scansione si fa una volta; dopo vengono elaborate solo le foto nuove.
- IT · ahora: Su un iPhone 13 con 15.000 foto, da 2,5 a 3 minuti. Su uno Xiaomi Mi A3 (Android di fascia media del 2019) con circa 8.000 foto, tra 4 e 5 minuti. Il tempo dipende dal telefono e da quante foto hai. La scansione si fa una volta; dopo vengono elaborate solo le foto nuove.

("El tiempo depende…" se añade porque dos mediciones no son una promesa: evita que alguien con un Android más lento o con 30.000 fotos lo lea como garantía.)

---

## 3. "Placa" → "placa electrónica" (solo ES)

### Elección del término

| Opción | España | Latinoamérica | Problema |
|---|---|---|---|
| **placa electrónica** | Se entiende | Se entiende | Ninguno serio; es genérico y cubre móviles, portátiles, electrodomésticos y climatización (los oficios del brief) |
| placa base | Muy usado | Se dice "tarjeta madre" o "placa madre" | Solo es la placa principal de un ordenador o móvil; deja fuera la placa de una lavadora o de un aire acondicionado |
| tarjeta electrónica | Poco usado | Común en México, Colombia (sobre todo electrodomésticos) | En España suena a tarjeta de crédito o SIM |
| placa de circuito | Técnico | Técnico | Suena a traducción de "circuit board" |
| board de laptop | No | Jerga de taller | Anglicismo, solo portátiles; el público general no lo entiende |

Elijo **"placa electrónica"**: es el único término que se entiende igual en España y en Latinoamérica y que abarca todos los oficios del brief. No puedo confirmar volúmenes de búsqueda; la elección es por claridad y cobertura, no por datos de palabras clave.

Regla de uso: término completo la primera vez en cada bloque de texto (cada respuesta de la FAQ se lee sola, sobre todo cuando la cita una IA); dentro del mismo bloque, "placas" a secas ya se entiende.

EN "circuit board" e IT "scheda elettronica" ya son específicos: **no cambian**.

### Cambios (ES)

**`home.hero.alt`**
- ES · antes: Un teléfono con iSIMILAR, rodeado de fotos de placas, planos y documentos
- ES · ahora: Un teléfono con iSIMILAR, rodeado de fotos de placas electrónicas, planos y documentos

**`home.pain.cards[0].p`**
- ES · antes: Placas, códigos de error, tuberías y reparaciones repartidas entre las fotos de tus hijos y tus vacaciones.
- ES · ahora: Placas electrónicas, códigos de error, tuberías y reparaciones repartidas entre las fotos de tus hijos y tus vacaciones.

**`how.sections[1].p`**
- ES · antes: Elige cualquier foto de tu galería o apunta la cámara a lo que tengas delante: una placa, un producto en el estante, un recibo. Los resultados aparecen en menos de un segundo, ordenados de más a menos parecidos.
- ES · ahora: Elige cualquier foto de tu galería o apunta la cámara a lo que tengas delante: una placa electrónica, un producto en el estante, un recibo. Los resultados aparecen en menos de un segundo, ordenados de más a menos parecidos.

**`how.limits[0]`**
- ES · antes: Encuentra por categoría, no por instancia: la foto de una placa devuelve placas en general, no la placa concreta de un cliente.
- ES · ahora: Encuentra por categoría, no por instancia: la foto de una placa electrónica devuelve placas en general, no la placa concreta de un cliente.

**`faq.items[4].a`** (duplicados; solo cambia el ejemplo)
- ES · antes: …iSIMILAR hace otra cosa: encuentra fotos que se parecen aunque no sean iguales, como placas de distintas reparaciones, productos del mismo estante o capturas con el mismo diseño…
- ES · ahora: …iSIMILAR hace otra cosa: encuentra fotos que se parecen aunque no sean iguales, como placas electrónicas de distintas reparaciones, productos del mismo estante o capturas con el mismo diseño…
- (Resto de la respuesta, idéntico. Sustitución exacta: "como placas de distintas reparaciones" → "como placas electrónicas de distintas reparaciones".)

**`faq.items[9].a`**
- ES · antes: No de forma fiable. Agrupa por parecido visual, por categoría: la foto de una placa devuelve placas en general, no la placa concreta de un cliente. Sirve para encontrar rápido y revisar, no para localizar una foto exacta.
- ES · ahora: No de forma fiable. Agrupa por parecido visual, por categoría: la foto de una placa electrónica devuelve placas en general, no la placa concreta de un cliente. Sirve para encontrar rápido y revisar, no para localizar una foto exacta.

Fuera de la web (solo lo reporto): la ficha de Google Play/App Store en español, los textos de capturas y los guiones de vídeo deberían usar el mismo término. Y un aviso no pedido: "no por instancia" (en `how.limits[0]`, las tres lenguas) es jerga técnica que el público general no entiende; propuesta para otra ronda: "encuentra el tipo de cosa, no la pieza concreta". No lo cambio aquí.

---

## 4. Detalle de la foto al abrir un resultado

⚠️ Contradicción detectada (omisión)
- Documento: `docs/definicion-tecnica.md` · Qué hace (puntos 1-6) no menciona que al abrir un resultado se vean fecha, tamaño en píxeles y peso. Sí dice, en Qué no es: "No busca por texto, fecha, ubicación ni cliente".
- Fuente: petición de Anibal (2026-10-23) dice: al abrir una imagen de los resultados se ve la fecha en que se tomó, el tamaño en píxeles y el peso.
- Impacto: la web describiría una función que el documento de referencia no recoge. Riesgo añadido: mostrar "fecha" junto a "no busca por fecha" puede leerse como que sí se puede filtrar por fecha.
- Opciones: A) ajustar la fuente al documento (no mencionarlo) · B) Anibal añade la función al documento (punto 4, "Acciones sobre los resultados", o uno nuevo)
- Esperando decisión.

Preguntas antes de publicar:
1. ¿Está en la versión publicada en las dos tiendas, en iOS y en Android? Si llega en una versión futura, mismo riesgo de calendario que compartir en lote (la web prometería algo que la app aún no hace).
2. ¿Qué fecha muestra exactamente? Si es la fecha de creación del archivo (lo habitual con photo_manager), en imágenes recibidas por WhatsApp, descargadas o capturas no es "la fecha en que se tomó" sino la fecha en que se guardó. Por eso escribo **"la fecha"** y no "la fecha en que se tomó". Si se confirma que es la fecha de captura (EXIF) con alternativa, se puede precisar.
3. ¿Es gratis? Supongo que sí (no es una acción en lote); el texto no lo dice, así que no compromete.

Dónde: `how.sections[3]` (Actúa sobre los resultados), al principio, porque abrir el detalle es lo que se hace antes de decidir. Le doy un uso concreto (elegir cuál conservar entre varias parecidas), que es por qué importa para el pilar **Ordena**; no menciono ordenar ni filtrar por fecha.

**`how.sections[3].p`** (el `h2` no cambia)
- EN · antes: Delete, move to a new or existing album, or share. You always see a preview and confirm before anything happens. Photos you move to an album stop showing up in later searches, so each search shows what's left to sort. On iPhone you can also remove a photo from an album without deleting it, and delete albums from the app.
- EN · ahora: Open any result to see the photo's details: its date, its size in pixels and its file size. It helps when you're choosing which of several similar photos to keep. Then delete, move to a new or existing album, or share. You always see a preview and confirm before anything happens. Photos you move to an album stop showing up in later searches, so each search shows what's left to sort. On iPhone you can also remove a photo from an album without deleting it, and delete albums from the app.
- ES · antes: Borra, mueve a un álbum nuevo o existente, o comparte. Siempre ves una vista previa y confirmas antes de que pase nada. Las fotos que mueves a un álbum dejan de aparecer en búsquedas posteriores, así cada búsqueda muestra lo que te queda por ordenar. En iPhone también puedes quitar una foto de un álbum sin borrarla y borrar álbumes desde la app.
- ES · ahora: Abre cualquier resultado para ver los detalles de la foto: la fecha, el tamaño en píxeles y el peso del archivo. Te ayuda a elegir cuál conservar entre varias fotos parecidas. Después, borra, mueve a un álbum nuevo o existente, o comparte. Siempre ves una vista previa y confirmas antes de que pase nada. Las fotos que mueves a un álbum dejan de aparecer en búsquedas posteriores, así cada búsqueda muestra lo que te queda por ordenar. En iPhone también puedes quitar una foto de un álbum sin borrarla y borrar álbumes desde la app.
- IT · antes: Elimina, sposta in un album nuovo o esistente, oppure condividi. Vedi sempre un'anteprima e confermi prima che succeda qualcosa. Le foto che sposti in un album non compaiono più nelle ricerche successive: così ogni ricerca ti mostra quello che resta da sistemare. Su iPhone puoi anche togliere una foto da un album senza eliminarla ed eliminare album dall'app.
- IT · ahora: Apri un risultato per vedere i dettagli della foto: la data, le dimensioni in pixel e il peso del file. Ti aiuta a scegliere quale tenere tra più foto simili. Poi elimina, sposta in un album nuovo o esistente, oppure condividi. Vedi sempre un'anteprima e confermi prima che succeda qualcosa. Le foto che sposti in un album non compaiono più nelle ricerche successive: così ogni ricerca ti mostra quello che resta da sistemare. Su iPhone puoi anche togliere una foto da un album senza eliminarla ed eliminare album dall'app.

"Peso" (ES/IT) es la palabra coloquial en España y Latinoamérica ("cuánto pesa la foto"); "peso del archivo" lo deja claro para quien no la usa.

**`faq.items[5].a`** (opcional, recomendado: cierra el malentendido con la fecha). Se añade una frase al final.
- EN · antes: Not for now. You always search from an image: a photo from your gallery or one taken with the camera. You can't type "beach 2019", and you can't search by date, location or client.
- EN · ahora: Not for now. You always search from an image: a photo from your gallery or one taken with the camera. You can't type "beach 2019", and you can't search by date, location or client. When you open a result you can see its date, but you can't search or filter by it.
- ES · antes: Por ahora, no. Siempre se busca desde una imagen: una foto de tu galería o una hecha con la cámara. No puedes escribir "playa 2019" ni buscar por fecha, ubicación o cliente.
- ES · ahora: Por ahora, no. Siempre se busca desde una imagen: una foto de tu galería o una hecha con la cámara. No puedes escribir "playa 2019" ni buscar por fecha, ubicación o cliente. Al abrir un resultado ves su fecha, pero no puedes buscar ni filtrar por ella.
- IT · antes: Per ora no. Si cerca sempre partendo da un'immagine: una foto della galleria o una scattata con la fotocamera. Non puoi scrivere "spiaggia 2019" né cercare per data, luogo o cliente.
- IT · ahora: Per ora no. Si cerca sempre partendo da un'immagine: una foto della galleria o una scattata con la fotocamera. Non puoi scrivere "spiaggia 2019" né cercare per data, luogo o cliente. Quando apri un risultato vedi la sua data, ma non puoi cercare o filtrare in base a quella.

(En el JSON las comillas internas van escapadas: `\"beach 2019\"`, como ya están.)

No lo pongo en portada ni en metadatos: es una ayuda para decidir, no un motivo de descarga.

---

## 5. Frase sobre confusiones

### Valoración honesta

La propuesta de Anibal tiene dos partes; una se puede usar y la otra no.

**"En algunos casos puede confundir imágenes de diferentes categorías"** — Sí, con matices:
- Es más cierta que la actual: la confusión no se limita a documentos y pantallas, y citar un solo caso puede dar a entender que no hay otros.
- "Categorías" es ambiguo para el usuario (¿categorías de la app?). Propongo "imágenes que se parecen pero son de distinto tipo".

**"La app trata de ponerlas al final de los resultados"** — **No se puede decir.** Lo verificable (definición técnica, punto 2) es que los resultados van "de más a menos parecidas". No hay ningún mecanismo que aparte los errores: una confusión es, por definición, una imagen que el modelo ve muy parecida, así que puede salir arriba. Afirmar lo contrario es una promesa falsa y además invita a borrar el final de la lista sin mirar el principio. Va contra el tono del brief ("honesto") y contra la regla de no prometer lo que no se comprueba.

**Quitar el dato concreto (1 de cada 5)** — Recomiendo **no** quitarlo del todo:
- El brief (línea 13) y la definición técnica (Límites) lo dan explícitamente; es el dato que justifica la regla "no decir 'encuentra todas tus facturas'".
- Las IA citan cifras concretas; "a veces se equivoca" es un descargo de responsabilidad que no dice nada y no se puede comprobar. La cifra es lo que hace creíble la honestidad de la marca.
- Para el segmento de recibos y documentos, saber cuál es el error típico es útil de verdad.
- Quitarlo de todas partes no contradice los documentos (es una omisión), pero desperdicia el único dato de error que tenemos.

**Propuesta:** frase general (la idea de Anibal) + el caso conocido como ejemplo. En portada, sin cifra (texto corto); en Límites y en la FAQ, con cifra. El 80% de acierto se mantiene donde está.

### Cambios

**`home.notDo.items[4]`**
- EN · antes: It gets it right about 80% of the time, and in about 1 in 5 cases it mixes up documents with photos of phone screens. Review before you delete.
- EN · ahora: It gets it right about 80% of the time. Sometimes it mixes up images that look alike but are different things, like documents and photos of phone screens. Review before you delete.
- ES · antes: Acierta en torno al 80% de las veces y, en uno de cada cinco casos aproximadamente, confunde documentos con fotos de pantallas de teléfono. Revisa antes de borrar.
- ES · ahora: Acierta en torno al 80% de las veces. A veces mezcla imágenes que se parecen pero son de distinto tipo, como documentos y fotos de pantallas de teléfono. Revisa antes de borrar.
- IT · antes: Ci azzecca circa 8 volte su 10 e in circa un caso su cinque confonde documenti e foto di schermi di telefono. Controlla prima di eliminare.
- IT · ahora: Ci azzecca circa 8 volte su 10. A volte confonde immagini che si somigliano ma sono di tipo diverso, come documenti e foto di schermi di telefono. Controlla prima di eliminare.

**`how.limits[2]`**
- EN · antes: Documents and photos of phone screens get mixed up in about 1 in 5 cases.
- EN · ahora: Sometimes it mixes up images that look alike but are different things. The best-known case is documents and photos of phone screens, mixed up in about 1 in 5 cases.
- ES · antes: Confunde documentos con fotos de pantallas de teléfono en uno de cada cinco casos, aproximadamente.
- ES · ahora: A veces mezcla imágenes que se parecen pero son de distinto tipo. El caso más conocido: documentos y fotos de pantallas de teléfono, que confunde en uno de cada cinco casos, aproximadamente.
- IT · antes: In circa un caso su cinque confonde documenti e foto di schermi di telefono.
- IT · ahora: A volte confonde immagini che si somigliano ma sono di tipo diverso. Il caso più noto: documenti e foto di schermi di telefono, confusi in circa un caso su cinque.

**`faq.items[8].q`** y **`faq.items[8].a`**
- EN · q · antes: Does it mix up documents with other photos?
- EN · q · ahora: Does it mix up different kinds of photos?
- EN · a · antes: Sometimes. In about 1 in 5 cases it mixes up documents with photos of phone screens (pictures taken of a phone's display, not screenshots). If you search from a document, expect a few of those among the results, and the other way around.
- EN · a · ahora: Sometimes. iSIMILAR compares how images look (shape, texture, color and composition), not what they show, so two different kinds of things can come up together if they look alike. The best-known case is documents and photos of phone screens (pictures taken of a phone's display, not screenshots): they get mixed up in about 1 in 5 cases. Review the results before deleting.
- ES · q · antes: ¿Confunde documentos con otras fotos?
- ES · q · ahora: ¿Confunde fotos de distinto tipo?
- ES · a · antes: A veces. En uno de cada cinco casos, aproximadamente, confunde documentos con fotos de pantallas de teléfono (fotos hechas a la pantalla de un móvil, no capturas de pantalla). Si buscas desde un documento, es normal que aparezca alguna de esas fotos entre los resultados, y al revés.
- ES · a · ahora: A veces. iSIMILAR compara cómo se ven las imágenes (forma, textura, color y composición), no lo que muestran, así que dos cosas distintas pueden salir juntas si se parecen. El caso más conocido son los documentos y las fotos de pantallas de teléfono (fotos hechas a la pantalla de un móvil, no capturas de pantalla): los confunde en uno de cada cinco casos, aproximadamente. Revisa los resultados antes de borrar.
- IT · q · antes: Confonde i documenti con altre foto?
- IT · q · ahora: Confonde foto di tipo diverso?
- IT · a · antes: A volte. In circa un caso su cinque confonde documenti e foto di schermi di telefono (foto scattate al display di un telefono, non screenshot). Se cerchi partendo da un documento, è normale trovarne qualcuna tra i risultati, e viceversa.
- IT · a · ahora: A volte. iSIMILAR confronta l'aspetto delle immagini (forma, texture, colore e composizione), non quello che mostrano, quindi due cose diverse possono comparire insieme se si somigliano. Il caso più noto sono i documenti e le foto di schermi di telefono (foto scattate al display di un telefono, non screenshot): li confonde in circa un caso su cinque. Controlla i risultati prima di eliminare.

Alternativa para la pregunta: mantener "documentos" en ella ("¿Confunde documentos u otros tipos de fotos?") si Anibal quiere conservar la búsqueda "documentos". Recomiendo la general: la respuesta ya nombra los documentos y la pregunta queda alineada con su petición.

No uso "los resultados se ordenan de más a menos parecidos" en esta respuesta: al lado de "se equivoca" sugiere que los errores quedan al final, que es justo lo que no podemos afirmar.

---

## 6. Sin publicidad

### Valoración

A favor: es un argumento real y verificable, respaldado por la política de privacidad publicada (apartado 1, las tres lenguas) y por la etiqueta de la App Store ("Sin rastreo ni publicidad", definición técnica). Encaja en el pilar **Privado**. "App sin anuncios" es además una búsqueda habitual.

Límites:
- **Nada sobre otras apps.** "A diferencia de otras apps llenas de anuncios engañosos" es una comparación que no podemos comprobar (brief, Tono). "Sin anuncios" ya hace el contraste solo, sin nombrar a nadie. El argumento de Anibal se puede enseñar en vídeo (la interfaz de iSIMILAR, limpia), sin decirlo.
- **No escribir "Sin rastreo / No tracking" suelto.** En la política está matizado ("en apps ni webs de otras empresas"). Suelto, en una etiqueta, se lee como "no recogemos nada", y el brief prohíbe "cero recopilación de datos": la app sí envía datos técnicos seudónimos a RevenueCat y Firebase. La frase completa solo va en la FAQ.
- Es un compromiso a futuro: si algún día se añade publicidad, hay que cambiar web, política y fichas a la vez.

### Dónde (de más a menos visible)

**a) `home.hero.badge`** — recomendado. Es lo primero que se lee y el formato ya es una lista de "sin…".
- EN · antes: Offline · No cloud · No account
- EN · ahora: Offline · No cloud · No account · No ads
- ES · antes: Sin internet · Sin nube · Sin cuenta
- ES · ahora: Sin internet · Sin nube · Sin cuenta · Sin anuncios
- IT · antes: Offline · Niente cloud · Nessun account
- IT · ahora: Offline · Niente cloud · Nessun account · Niente pubblicità

Riesgo: en IT pasa a 59 caracteres y en ES a 51; comprobar en un teléfono de 360 px que la etiqueta no se parte mal. Si se parte, alternativa: sustituir `home.stats[2]` ("No account needed / Sin cuenta / Nessun account", que ya repite la etiqueta) por "No ads / Sin anuncios / Niente pubblicità" y dejar la etiqueta como está.

**b) Pregunta nueva en la FAQ, insertada como `faq.items[3]`** (después de "¿Qué datos recoge la app?") — recomendado. Es el formato que mejor citan las IA y lleva la frase completa y matizada.
- EN · q: Does iSIMILAR show ads?
- EN · a: No. There are no ads in the app, in the free version or in PRO. iSIMILAR doesn't track you across other companies' apps or websites, doesn't collect your phone's advertising identifier (IDFA on iPhone, Advertising ID on Android) and doesn't sell your data. The app makes money only from the PRO subscription.
- ES · q: ¿iSIMILAR tiene anuncios?
- ES · a: No. La app no muestra publicidad, ni en la versión gratuita ni en PRO. iSIMILAR no te rastrea en apps ni webs de otras empresas, no recoge el identificador publicitario del teléfono (IDFA en iPhone, ID de publicidad en Android) y no vende tus datos. La app se financia solo con la suscripción PRO.
- IT · q: iSIMILAR ha pubblicità?
- IT · a: No. L'app non mostra pubblicità, né nella versione gratuita né in PRO. iSIMILAR non ti traccia su app o siti di altre aziende, non raccoglie l'identificativo pubblicitario del telefono (IDFA su iPhone, ID pubblicità su Android) e non vende i tuoi dati. L'app si finanzia solo con l'abbonamento PRO.

Efecto de la inserción: todos los `faq.items` desde el actual [3] suben un puesto. **Cambiar también `home.faqPreview.items`** en los tres idiomas:
- EN/ES/IT · antes: [1, 4, 7]
- EN/ES/IT · ahora: [1, 5, 8]
(Así la portada sigue mostrando "¿Mis fotos salen del teléfono?", "¿Es un limpiador de duplicados?" y "¿Cuánto acierta?".) Alternativa sin tocar índices: añadir la pregunta al final de la lista; peor sitio, pero cero riesgo.

**c) `how.privacyP`** — opcional. Se añade una frase antes del enlace a la política (el texto termina justo donde empieza el enlace).
- EN · antes: …The app sends technical data on purchases, usage and errors, never photos or gallery content. Details in the
- EN · ahora: …The app sends technical data on purchases, usage and errors, never photos or gallery content. There are no ads, and the app doesn't collect your advertising identifier. Details in the
- ES · antes: …La app envía datos técnicos de compras, uso y errores, sin fotos ni contenido de la galería. Los detalles, en la
- ES · ahora: …La app envía datos técnicos de compras, uso y errores, sin fotos ni contenido de la galería. No hay publicidad y la app no recoge el identificador publicitario. Los detalles, en la
- IT · antes: …L'app invia dati tecnici su acquisti, utilizzo ed errori, mai foto o contenuti della galleria. I dettagli sono nell'
- IT · ahora: …L'app invia dati tecnici su acquisti, utilizzo ed errori, mai foto o contenuti della galleria. Niente pubblicità, e l'app non raccoglie l'identificativo pubblicitario. I dettagli sono nell'
- (El principio del texto, "Your photos and their thumbnails…", no cambia.)

No lo pongo en el H1 ni en los metadatos: el mensaje principal sigue siendo **Encuentra**; "sin anuncios" refuerza, no vende solo.

### Para revisión de `legal-tiendas` (marcado)

1. **"No recoge el identificador publicitario"** (FAQ nueva y `how.privacyP`). La política ya lo dice, pero la web lo amplifica. La definición técnica solo documenta la retirada del permiso `AD_ID` como parte de la configuración de Firebase Analytics, que está fuera de la app. Hay que confirmar en la versión publicada que el manifiesto final de Android no declara `com.google.android.gms.permission.AD_ID` (puede entrar por dependencias) y que RevenueCat no llama a `collectDeviceIdentifiers`. No puedo confirmarlo desde aquí.
2. **"La app se financia solo con la suscripción PRO"**: es cierto según la definición técnica ("El único producto es una suscripción anual"), pero es un compromiso comercial público. Revisar si se quiere asumir.
3. Coherencia con las fichas: Google Play debe declarar "Contiene anuncios: No" y la etiqueta de la App Store, sin publicidad. Si alguna dijera otra cosa, la web no puede publicarse con estos textos.

---

## 7. Revisión de tono (skill `tono-de-marca`)

| Frase | Problema | Regla | Resultado |
|---|---|---|---|
| "buscador privado de imágenes similares" | Puede atraer búsquedas de búsqueda inversa en internet | Brief: "No es Google Lens" | Apto: siempre con "privado" y "galería del teléfono"; títulos sin cambiar |
| "Xiaomi Mi A3 … entre 4 y 5 minutos" | Dato que el documento da como "sin medir" | Definición técnica, Rendimiento medido | Apto si Anibal actualiza el documento (contradicción del punto 2) |
| "placa electrónica" | Ninguno | Idioma natural del mercado | Apto |
| "Abre cualquier resultado… la fecha…" | Función no documentada; "fecha" podría sugerir búsqueda por fecha | Definición técnica, Qué hace / Qué no es | Apto con cambios: "la fecha" (no "en que se tomó") y frase en FAQ[5] |
| "la app trata de ponerlas al final" (propuesta de Anibal) | Promesa no verificable | Definición técnica, punto 2; brief, Tono | No apto: no se usa |
| "A veces mezcla imágenes… como documentos y pantallas… 1 de cada 5" | Ninguno | Brief, línea 13 | Apto |
| "No ads / Sin anuncios" | Ninguno; respaldado por la política | Brief, pilar Privado | Apto |
| "Sin rastreo" suelto | Se lee como "cero recopilación" | Brief, tabla "no se puede decir" | No se usa suelto; solo la frase completa en la FAQ |
| "A diferencia de otras apps con anuncios" | Comparación no verificable | Brief, Tono | No se usa |

Pilares: 1 y 3 → Encuentra; 2 → expectativa honesta; 4 → Ordena; 5 → honestidad (acierto); 6 → Privado. Sin "magia", superlativos, "el primero", "exacta", "0,5 s" ni "anónimo". Precio y PRO, sin cambios.

**Veredicto: apto con cambios** (los marcados arriba y las decisiones de la sección 8).

---

## 8. Qué tiene que decidir Anibal

1. Punto 1: ¿quitar "visual" ("buscador privado de imágenes similares") o mantenerlo? ¿Cambiar también `home.meta.description`? ¿Adopta el brief la nueva definición?
2. Punto 2: actualizar `docs/definicion-tecnica.md` con la medición del Mi A3 antes de publicar (opción B) y responder las preguntas de la medición.
3. Punto 4: confirmar que el detalle de foto está publicado en iOS y Android, qué fecha muestra, y añadirlo al documento (opción B). ¿Añadir la frase a `faq.items[5]`?
4. Punto 5: aceptar que "la app las pone al final" no se publica y que la cifra 1 de cada 5 se mantiene en Límites y FAQ.
5. Punto 6: ¿etiqueta del hero o franja de datos? ¿FAQ nueva insertada (con `faqPreview` → [1, 5, 8]) o al final? Pasar los 3 puntos marcados a `legal-tiendas` antes de publicar.

Rollback: todos los cambios son de `en.json`, `es.json` e `it.json`; se deshacen con `git revert` del commit en `solopila_landingPAGE/`.
