# Capturas de la App Store · Encargo para Claude Design

Borrador de `growth` · 2026-10-24 · Estado: **pendiente de revisión de Anibal**
Alcance: **solo App Store** (iPhone). Fuentes: `docs/brief-marketing.md` (Guía para las capturas de la tienda), `docs/guia-estrategica.md` (Auditoría de la ficha, Prioridades 2, semanas 3–4), `docs/definicion-tecnica.md`, `borradores/pendientes.md` y `borradores/2026-10-23-web-ajustes-growth.md`.

**Hipótesis:** si las tres primeras capturas muestran el resultado con fotos de trabajo, en lugar del permiso, el botón de escaneo y la barra de progreso, sube la conversión desde la búsqueda de la App Store.
**Cómo se mide:** en App Store Connect › App Analytics: tasa de conversión (descargas / impresiones únicas) y visitas a la ficha / impresiones, con origen "App Store Search" y territorio EE. UU. Se comparan las 4 semanas anteriores con las 4 posteriores. Con 500–1.850 impresiones al mes no habrá significación estadística, así que es una lectura de tendencia. La prueba real es la A/B de capturas (guía, semanas 3–4).
**Cuándo se decide:** 4 semanas después de que la versión con las capturas nuevas esté aprobada.

---

## 1. Requisitos de la App Store (verificados el 2026-10-24)

Fuente: https://developer.apple.com/help/app-store-connect/reference/app-information/screenshot-specifications

| Requisito | Qué dice Apple hoy |
|---|---|
| Tamaño obligatorio | "To submit your app, you must provide screenshots for the following required display sizes: iPhone: At least one screenshot for iPhone with Dynamic Island (medium display)." |
| Dynamic Island, pantalla mediana (≈6,1–6,3") | 1179×2556 o 1206×2622 (vertical) |
| Dynamic Island, pantalla grande (≈6,9") | 1260×2736, 1290×2796 o 1320×2868. No es obligatorio, pero si falta, Apple exige el de 6,5" |
| Face ID, pantalla grande (≈6,5") | 1242×2688 o 1284×2778. "Required if app runs on iPhone and screenshots for iPhone with Dynamic Island (large display) aren't provided" |
| Face ID, pantalla mediana (iPhone 13) | 1170×2532: es un tamaño válido, pero no el obligatorio |
| Número | De 1 a 10 por tamaño: "at least one screenshot and can upload up to 10 screenshots per device size" |
| Formato | `.jpeg`, `.jpg` o `.png`. "Images can't include alpha channels or transparencies" |
| Contenido (guía 2.3.3) | "Screenshots should show the app in use… They may also include text and image overlays" (https://developer.apple.com/app-store/review/guidelines/) |
| Contenido (guía 2.3.10) | Nada de nombres, iconos ni imágenes de otras plataformas móviles (Android) en los metadatos |

**Qué entregar:** las 6 capturas en **1320×2868** (6,9") y en **1206×2622** (mediana, la obligatoria). Así se cumplen las dos frases de Apple, que se contradicen entre sí (ver punto 2). Las dos proporciones son casi iguales (0,4603 y 0,4600), así que es el mismo diseño exportado dos veces. En total: 6 capturas × 3 idiomas × 2 tamaños = **36 PNG sin alfa**.

**Lo que no pude verificar:**
- La página no tiene fecha de actualización. El tamaño obligatorio "mediano" con Dynamic Island cambia respecto a lo que exigía Apple antes (6,9"). Conviene confirmarlo en App Store Connect al subir.
- Las dos frases de Apple chocan: el tamaño mediano es "required", pero esa misma sección dice que, si falta, se escala desde el de 6,5". Entregando los dos tamaños da igual.
- No sé si Claude Design exporta PNG con medidas exactas y sin canal alfa. Hay que comprobarlo en cada archivo antes de subirlo (en el Mac: `sips -g pixelWidth -g pixelHeight -g hasAlpha archivo.png`).
- Las capturas son metadatos de la versión: según lo que sé, solo se cambian al enviar una versión nueva (la A/B de capturas es la excepción). No lo he verificado hoy.
- No he comprobado la licencia de los marcos oficiales de Apple (Apple Design Resources › Product Bezels), ni si incluyen el iPhone 13.

## 2. Las 6 capturas

Orden y escenas del brief. Las capturas del iPhone 13 (1170×2532) se reducen al encajarlas en el marco; nunca se amplían, así que la calidad aguanta.

| # | Pantalla de la app | Fotos en la galería para esa escena | Estado de la app | EN | ES | IT | ¿Sirve la captura de la 1.1.6? |
|---|---|---|---|---|---|---|---|
| 1 | Resultados de una búsqueda con cámara (cuadrícula + "Similar images: N"), con un recuadro pequeño de la foto de la placa hecha con la cámara | 40 o más fotos de placas de reparaciones distintas, mezcladas con fotos personales | Escaneo terminado; búsqueda real, orden "más parecidas" | Find photos like this one | Encuentra fotos parecidas a esta | Trova foto simili a questa | Sí, si se ven placas reales y ningún contador de "free actions". Si no, rehacer |
| 2 | Visor del álbum "Work / Trabajo / Lavoro" con las fotos movidas, o el aviso "Album … created with N images" | 100 o más fotos de trabajo (placas, móviles abiertos, pantallas rotas fotografiadas) + fotos personales neutras | Acción en lote hecha (PRO); el número del aviso es real | Separate work from personal | Separa trabajo y vida personal | Separa lavoro e vita privata | Sí, si muestra trabajo y no hay contador de acciones gratis. Rehacer si el álbum es de perros o comida |
| 3 | Segunda búsqueda lanzada desde un resultado de la primera (búsqueda en cadena) | 30 o más fotos de productos del supermercado (arroz, salsas, pasta) | Resultados de la 2.ª búsqueda; si la app lo permite, un recuadro con la 1.ª | Search again from any result | Sigue buscando desde cualquier resultado | Cerca ancora da qualsiasi risultato | Probablemente sí, si existe con productos. No sé qué fotos tienen las actuales |
| 4 | Resultados en modo selección, con cientos de fotos marcadas y la barra de borrar | 200 o más memes, saludos y capturas con el mismo formato | Selección real (p. ej. "312 selected"), antes de confirmar | Delete hundreds at once | Borra cientos de una vez | Elimina centinaia in un colpo | **Rehacer** si la barra muestra "5 free actions" o un contador de créditos (la guía dice que las capturas actuales lo muestran) |
| 5 | Cualquier resultado con el icono de modo avión en la barra de estado; el diseño añade una lupa ampliada sobre ese icono | Las mismas placas de la escena 1 | Modo avión activo y Wi‑Fi apagado; búsqueda terminada | Works offline. Photos stay local | Sin internet y sin nube | Senza internet e senza cloud | Sí, si existe una con el modo avión visible. Si no, se hace en 2 minutos |
| 6 | Muro de pago de la **versión nueva** | No aplica | Muro abierto desde una acción en lote | Search free. Batch with PRO | Busca gratis. Lote con PRO | Cerca gratis. In blocco, PRO | **Rehacer con la versión nueva** (T5–T8). El muro de la 1.1.6 tiene textos prohibidos por el brief |

Notas de las escenas:
- **Etiqueta PRO en las escenas 2 y 4 (recomendada):** una píldora pequeña "PRO" junto al titular. Así nadie descarga creyendo que el lote es gratis, que es justo lo que hacía el antiguo "5 free actions". Decide Anibal (pregunta 3).
- **Idioma de la interfaz:** lo ideal es que las capturas ES e IT muestren la app en ES e IT ("Imágenes similares:", "Immagini simili:"). Basta con cambiar el idioma del iPhone y repetir la misma escena. Si no hay tiempo, el titular se traduce y la interfaz queda en inglés. Apple lo acepta, pero convence menos.
- **Las cuadrículas no se retocan:** son resultados reales. Con un 80% de acierto, puede colarse alguna foto que no se parece; se elige una búsqueda limpia, pero no se borran miniaturas en el diseño.
- **Escena 6, precio:** el muro muestra el precio de un país (p. ej. 11,99 USD), pero esa captura sale en todas las tiendas. Recomiendo tapar el precio o encuadrar sin él (pregunta 4).

## 3. Fotos que Anibal debe tener en el teléfono

| Escena | Qué fotografiar o tener | Cantidad orientativa |
|---|---|---|
| 1 y 5 | Una placa sobre la mesa de trabajo (para la cámara) + fotos de placas de reparaciones distintas, con luz y fondo parecidos | 40+ |
| 2 | Fotos de trabajo: placas, móviles abiertos, pantallas rotas (fotos de pantallas físicas). Y fotos personales neutras: paisajes, comida, objetos | 100+ trabajo, 50+ personales |
| 3 | Productos del supermercado: arroz, salsas, pasta | 30+ |
| 4 | Memes, saludos de "buenos días" y capturas con el mismo diseño | 200+ |
| 6 | Ninguna: el muro de la versión nueva | — |

**⚠️ Privacidad antes de hacer cada captura (y antes de subir nada a Claude Design):**
- Subir las capturas a Claude Design las envía a un servidor. Solo deben salir del teléfono capturas **ya limpias**.
- Tapar o desenfocar en el propio iPhone, nunca en el diseño: emails, contraseñas, nombres y teléfonos de clientes, IMEI y números de serie, matrículas, direcciones, nombres de contactos de WhatsApp y notificaciones.
- Ninguna cara reconocible, y menos de menores, ni siquiera en miniatura.
- No mencionar ni mostrar que se fotografían emails o contraseñas de clientes (decisión de Anibal, 2026-10-23).
- **Propiedad intelectual:** nada de memes con personajes o logotipos de terceros en la escena 4 (mejor saludos hechos por Anibal o capturas sin marcas). En la escena 3, ningún logotipo grande como foto base. La guía 5.2 de Apple prohíbe material de terceros sin permiso en los metadatos. No sé con qué rigor lo aplican a logotipos de fondo en miniaturas.
- Barra de estado: sin operador y con la batería alta. En la escena 5 debe verse el icono del avión.

## 4. Identidad visual (de `solopila_landingPAGE/astro/src/styles/global.css` y `layouts/Base.astro`)

- Fondo `#0D0F12` · tarjetas `#1A1D24` · verde `#39FF14` · cian `#00B4D8` · texto `#FFFFFF` · texto secundario `#94A3B8` · líneas `rgba(255,255,255,.08)` · texto sobre verde `#031200`.
- Degradado de marca: `linear-gradient(90deg, #39FF14, #00B4D8)`. Brillo de fondo: radial cian `rgba(0,180,216,.22)` arriba y verde `rgba(57,255,20,.1)` a un lado. Rejilla de líneas cada 56 px que se desvanece.
- Tipografía: **Inter** (Google Fonts), titulares en peso 800 con interletraje −0,03 a −0,045 em; texto en 500–600.
- Marco del teléfono con borde degradado cian → verde y sombra cian, como `.show` de la web.

## 5. Prompt para pegar en Claude Design

```
Diseña 6 capturas para la App Store (iPhone) de iSIMILAR, un buscador privado de imágenes similares para la galería del teléfono. Te adjunto 6 capturas reales de un iPhone 13 (1170×2532), numeradas 1 a 6, en EN, ES e IT. Genera 18 diseños: 6 escenas × 3 idiomas.

LIENZO
- Vertical, 1320×2868 px (iPhone 6,9"). Después, exporta cada diseño también a 1206×2622 px (la proporción es casi la misma: reescala sin recolocar).
- PNG opaco, sin transparencias ni canal alfa. Nombres: isimilar-{idioma}-{n}-{tamaño}.png (ej.: isimilar-es-1-1320x2868.png).

ESTILO (sacado de la web isimilar.app)
- Fondo #0D0F12 con un brillo radial cian rgba(0,180,216,.22) arriba y otro verde rgba(57,255,20,.10) a un lado, más una rejilla sutil de líneas rgba(255,255,255,.08) cada 56 px que se desvanece hacia abajo.
- Tipografía Inter. Titular en peso 800, blanco #FFFFFF, interletraje −0,035 em, interlineado 1,05, de 110 a 130 px, centrado y en 1 o 2 líneas como máximo. Una palabra clave del titular puede llevar el degradado #39FF14 → #00B4D8. Una sola palabra por captura, siempre en la misma posición lógica.
- Acentos: verde #39FF14, cian #00B4D8 y texto secundario #94A3B8. Nada más.

JERARQUÍA Y COMPOSICIÓN (idéntica en las 18)
- Arriba, el titular en el 22% superior del lienzo, con margen lateral de 90 px. Ningún subtítulo: solo el titular.
- Debajo, la captura dentro de un marco de iPhone con muesca (como el iPhone 13), de unos 1.000 px de ancho. El marco va centrado y puede salir por el borde inferior. Borde fino con degradado cian → verde y sombra cian suave. La captura se reduce, nunca se amplía, y no se recorta la barra de estado.
- No retoques el contenido de las capturas: ni miniaturas ni números. Solo puedes añadir los elementos indicados abajo.
- Sin flechas, manos ni dedos, botones de descarga, insignias de tienda, logotipos de Android o de terceros, ni palabras como "best", "#1", "new" o "free" fuera del titular.

ELEMENTOS POR ESCENA
1. Captura 1 (resultados). Añade un recuadro redondeado pequeño, arriba a la izquierda del teléfono, con la foto de la placa hecha con la cámara (recórtala de la captura 1b que te adjunto), unido a la cuadrícula por una línea fina cian.
2. Captura 2 (álbum de trabajo). Píldora "PRO" pequeña (fondo rgba(57,255,20,.12), texto #39FF14, peso 700, mayúsculas) bajo el titular.
3. Captura 3 (búsqueda en cadena). Sin elementos extra.
4. Captura 4 (selección en lote). La misma píldora "PRO" bajo el titular.
5. Captura 5 (modo avión). Un círculo ampliado (lupa) que aumenta el icono de modo avión de la barra de estado de la propia captura, y un candado CERRADO pequeño, de línea, en #39FF14, junto al titular. Nunca un candado abierto.
6. Captura 6 (muro de pago). Sin elementos extra. Si se ve un precio, tápalo con una franja del color de la tarjeta (#1A1D24).

TITULARES (exactos, no los cambies ni los traduzcas tú)
| n | EN | ES | IT |
| 1 | Find photos like this one | Encuentra fotos parecidas a esta | Trova foto simili a questa |
| 2 | Separate work from personal | Separa trabajo y vida personal | Separa lavoro e vita privata |
| 3 | Search again from any result | Sigue buscando desde cualquier resultado | Cerca ancora da qualsiasi risultato |
| 4 | Delete hundreds at once | Borra cientos de una vez | Elimina centinaia in un colpo |
| 5 | Works offline. Photos stay local | Sin internet y sin nube | Senza internet e senza cloud |
| 6 | Search free. Batch with PRO | Busca gratis. Lote con PRO | Cerca gratis. In blocco, PRO |

CONSISTENCIA
- Primero diseña la escena 1 en EN como plantilla maestra y enséñamela. Cuando la apruebe, aplica exactamente la misma retícula, tamaños, márgenes, posición del teléfono y estilo a las otras 17. Solo cambian el titular, la captura y los elementos de cada escena.
- Si un titular en ES o IT no cabe en 2 líneas al tamaño de la plantilla, baja el cuerpo de letra en todo ese idioma a la vez, no solo en esa captura.
- Al final, muéstrame las 18 en una tabla de 6 columnas (escenas) × 3 filas (idiomas) para revisarlas juntas.
```

## 6. Revisión `tono-de-marca` (titulares)

| Frase | Problema | Regla | Versión entregada |
|---|---|---|---|
| "Find photos that look like this" (brief) | 6 palabras | Brief: titulares de 5 palabras o menos | "Find photos like this one" (contradicción abajo) |
| "Separate work from personal" / ES / IT | Podría sonar automático | Brief: no "separa automáticamente" | Válido: la escena muestra al usuario moviendo las fotos. Lleva PRO |
| "Delete hundreds at once" | Es una acción en lote, que es PRO | Brief, Precio | Píldora PRO; el número de la captura es real |
| "Sin internet y sin nube" | Ninguno | Frase central del brief ("sin internet y sin nube") | Apto |
| "Search free" / "Busca gratis" / "Cerca gratis" | La cámara solo tiene 5 búsquedas gratis | Brief: "Búsqueda gratis para siempre" se permite; "gratis" a secas no | Apto: "gratis" va pegado a "buscar". Las búsquedas desde la galería son ilimitadas |
| "Cerca gratis. In blocco, PRO" | Elíptico en italiano | Idioma natural del mercado | Apto con cambios: que lo revise un nativo. Alternativa de 6 palabras: "Cerca gratis. In blocco con PRO" |

Pilares: 1 y 3 Encuentra · 2 y 4 Ordena · 5 Privado · 6 Precio. Sin "magia", "exacta", "instantly", "100%", cifras inventadas ni "5 free actions". **Veredicto: apto con cambios** (contradicción 1 y revisión nativa del IT de la escena 6).

## 7. Contradicciones y riesgos

⚠️ Contradicción detectada
- Documento: `docs/brief-marketing.md` · Guía para las capturas de la tienda dice: titular 1 "Find photos that look like this" y, en las reglas, "titulares de cinco palabras o menos".
- Fuente: el propio brief (la misma sección) dice: el titular orientativo 1 tiene 6 palabras.
- Impacto: el titular de la captura más vista incumple la regla del brief.
- Opciones: A) usar "Find photos like this one" (5 palabras, mismo sentido; es lo que lleva el prompt) · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada
- Documento: `docs/brief-marketing.md` · Guía para las capturas de la tienda dice: la captura 3 es la "Búsqueda en cadena con productos del supermercado".
- Fuente: `docs/guia-estrategica.md` · Semanas 1–2 dice: "Rehacer las tres primeras capturas para que muestren el resultado con fotos reales de trabajo: placas, pantallas, reparaciones"; y Prioridades 2: las tres primeras son "la cámara apuntando a una placa, las fotos parecidas encontradas y el traslado en lote a un álbum".
- Impacto: cambia qué ve quien no abre la ficha (las tres primeras capturas).
- Opciones: A) seguir el brief (es lo que lleva este borrador) · B) Anibal revisa el documento (por ejemplo, la 3 con trabajo y el supermercado en la 4)
- Esperando decisión.

⚠️ Contradicción detectada
- Documento: `docs/brief-marketing.md` · Lo que se puede y no se puede decir dice: no "encuentra cualquier foto al instante", no superlativos, "Tus fotos nunca salen del teléfono" en lugar de "100%".
- Fuente: `solopila/lib/l10n/intl_en.arb:326-346` (muro de pago actual) dice: "100% offline. 100% private.", "Find any photo instantly", "finds every related photo".
- Impacto: la captura 6 no puede usar el muro actual. Ya está previsto en T5–T8 (`borradores/2026-10-22-instrucciones-app.md`); la captura 6 depende de esa versión.
- Opciones: A) ajustar la fuente al documento (T5–T8, ya pendiente) · B) Anibal revisa el documento
- Esperando decisión.

Riesgos:
- **Calendario:** las capturas 2, 4 y 6 enseñan acciones en lote y el muro nuevo. Si se suben antes de que la versión nueva esté aprobada, la captura 6 enseña una pantalla que la app publicada no tiene. Se suben con esa versión.
- **El código actual sigue llevando "free actions":** `intl_*.arb:510-530` (`free_actions_label`, `low_free_actions_status`: "Get credits to continue"). La definición técnica dice que son restos sin uso. No he comprobado que no se muestren en ninguna pantalla de la versión nueva: hay que revisarlo en cada captura rehecha.
- **Muesca frente a Dynamic Island:** se suben capturas de iPhone 13 (con muesca) en el hueco de iPhones con Dynamic Island. Apple escala; no conozco ninguna regla que lo prohíba, pero el marco debe ser de un iPhone con muesca para que no se vea raro.
- **Volumen bajo:** no habrá significación estadística en 4 semanas. No hay que sacar conclusiones fuertes de una subida o bajada.

## 8. Preguntas para Anibal

1. ¿En qué idioma está la interfaz de tus capturas de la 1.1.6? ¿Repites las escenas con el iPhone en ES e IT, o la interfaz va en inglés con el titular traducido?
2. ¿Qué muestran hoy tus capturas (placas, supermercado, memes, modo avión)? Con eso cierro la columna "¿Sirve?" escena por escena.
3. ¿Píldora "PRO" en las escenas 2 y 4? Recomiendo que sí.
4. Escena 6: ¿se tapa el precio o se encuadra sin él? Va ligado a la decisión de precio pendiente.
5. Contradicciones 1 y 2: ¿A o B?
6. ¿Quién revisa el italiano (escena 6 sobre todo) antes de exportar?

---
Google Play: pendiente, con capturas de Android.

## Revisión de las capturas de Anibal (EN, 2026-10-24)
Carpeta: `archivo/Imagenes_APP_iSIMILAR/Ingles/` (1170×2532, interfaz en inglés, versión 1.1.6).
Respuestas de Anibal: etiqueta PRO en 2 y 4: sí · precio tapado en la 6: sí · revisa el italiano: Anibal.

| Imagen | Uso propuesto | Nota |
|---|---|---|
| 5.PNG | Captura 1 | Placa, 162 resultados. La mejor |
| 4.PNG | Captura 2 + PRO | Todas seleccionadas, Delete / Save Image |
| 7.PNG | Captura 3 | Detalle con "Search similar". Desenfocar pegatinas con código de barras / n.º de serie |
| 6.PNG | Extra (7) | Menú de orden |
| 8.PNG | No usar | Débil |
| 1, 3.PNG | No usar | Textos "Find every…" y "Scans… instantly" contrarios al brief |
| 2.PNG | No usar | Barra de progreso |
| 9, 10.PNG | No usar | Marcas de terceros (Tabasco, Tampax, Dash, Gillette…) |
| 11, 12.PNG | Opcional | Leche de almendras; desenfocar marca |

Faltan: captura 4 (borrado en lote con fotos propias, sin memes), captura 5 (modo avión
visible), captura 6 (muro, con la versión nueva), "1b" cámara apuntando a una placa (o quitar
el recuadro del prompt). Anibal debe repetir las válidas en ES e IT.

Vídeo `VIDEO_BUSQUEDAS.mov` (18,75 s): de 0,5 s a 4,25 s sale el selector de Fotos de iOS con
fotos personales (una cara, carteles, muro antiguo con $11.99). Quitarlo. Si se corta queda
en ~15 s (mínimo de App Store, sin verificar hoy). Opciones: A) cortar y alargar el final ·
B) desenfocar el selector. Para la ficha: convertir a 886×1920. Falta saber el destino
(ficha de App Store o redes).

Pendiente: ajustar el prompt de Claude Design con este reparto cuando Anibal decida las dos
contradicciones (titular 1 de 6 palabras; captura 3 con trabajo en vez de supermercado).

## Decisiones de hq (2026-10-31) · se hacen con la versión nueva (app lista)
- Contradicción 1: **A**, "Find photos like this one" (5 palabras).
- Contradicción 2: la captura 3 es la **búsqueda en cadena con fotos de trabajo** (7.PNG o
  nueva), que cumple el brief (cadena) y la guía (trabajo en las 3 primeras). El supermercado
  queda como opcional (11/12.PNG, marca desenfocada).
- Contradicción 3: resuelta por T5–T9 (muro sin textos prohibidos).
- Restos de "free actions" en el código: ya no existen (comprobado en `solopila/lib`).
- Orden: capturas y ficha **antes** de enviar la versión. En App Store las capturas van con
  la versión; en Google Play se pueden cambiar en cualquier momento.
- Pendiente de hacer con la app nueva (iPhone, en EN, ES e IT): captura 4 (borrado en lote
  con fotos propias, ~100+ seleccionadas), captura 5 (modo avión visible), captura 6 (muro
  nuevo, precio tapado), y repetir 1–3 en ES e IT.

## Tamaños y marcos (hq, 2026-11-09)
Solo hay un iPhone 13 (1170 × 2532 px, pantalla de 6,1"), con más de 15.000 fotos reales.
Ninguna tienda acepta esa captura tal cual, así que **todas las capturas van dentro de un marco**:
la captura reducida, con el titular encima y un fondo de marca en el espacio que sobra.

| Tienda | Tamaño del marco | Por qué |
|---|---|---|
| App Store | **1290 × 2796** (6,9") | Apple pide un solo juego, de 6,9" o 6,5", y lo escala a los demás. 6,1" no está entre los aceptados. |
| Google Play | **1080 × 1920** (9:16) | El lado largo no puede pasar del doble del corto; la captura del iPhone (2,16:1) no cumple. |

- Mismo diseño en las dos tiendas, adaptado a cada proporción.
- **Para Google Play:** sin marco de iPhone ni elementos propios de iOS a la vista (la barra de
  estado, recortada o neutra). No he confirmado si Google lo rechaza; se evita por prudencia.
- Comprobar en App Store Connect (biblioteca de capturas) los tamaños vigentes al subir.
Fuentes: developer.apple.com (Screenshot specifications) y support.google.com (Play Console,
answer 9866151).
