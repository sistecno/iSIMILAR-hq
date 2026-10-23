# Ficha de App Store y respuesta de precisión del muro de pago

Fecha: 22-10-2026 · Agente: growth · Estado: borrador para que Anibal decida

Fuentes leídas: `docs/brief-marketing.md` (la cabecera del archivo dice "Actualizado el Oct 21, 2026"), `docs/guia-estrategica.md` (sección "La ficha de la App Store"), `docs/definicion-tecnica.md` (velocidad, precisión, GPU), `../solopila/lib/l10n/intl_{en,es,it}.arb` y `../solopila/lib/services/embedding_service.dart`.

---

## Cómo se obtuvo la descripción publicada (léelo antes de pegar nada)

- En esta sesión no tengo terminal, así que **no pude usar curl**. WebFetch sobre `apps.apple.com` solo devolvió un resumen.
- Saqué el texto línea a línea de la API pública de Apple (`itunes.apple.com/lookup?id=6738889078&country=us|es|it`). La herramienta corta las citas largas, así que:
  - **EN:** tengo literales todas las líneas salvo tres párrafos (3, 5 y 17), que reconstruí uniendo dos fragmentos. Las palabras son exactas, pero **no puedo confirmar la puntuación en la unión** (marcada con `[unión]`).
  - **ES e IT:** las devolvió completas, pero partidas en trozos. **No puedo confirmar los saltos de línea ni las líneas en blanco exactas.**
- **Por tanto: no pegues la descripción completa desde aquí.** Abre la de App Store Connect y aplica solo los cambios "actual → nuevo". La descripción completa que hay más abajo sirve como referencia.
- Nota de ASO: en iOS la descripción **no cuenta para el posicionamiento en la búsqueda** (cuentan el título, el subtítulo y las palabras clave). Corregirla importa por dos motivos: la gente que llega a leerla, y que ChatGPT y otros asistentes la leen y repiten. Hoy pueden repetir "~50 ms" y "doctors / X-rays".

---

## Tarea 1. Descripción de App Store

⚠️ Contradicción detectada
- Documento: `docs/brief-marketing.md` · "Para quién" ("Perfiles que no se usan como mensaje principal: sanitarios…") y "Lo que se puede y no se puede decir" ("encuentra cualquier foto al instante", "Nada de magia") dice: no se usan sanitarios, no se promete la foto exacta, no se usa "magia" y no se dan cifras sin datos.
- Fuente: ficha de App Store EN/ES/IT (descripción publicada, v1.1.6) dice: "Doctors/Engineers: Photograph X-rays…", "the teardown photos you took 4 months ago", "~50 ms, even with 15,000+ photos", "THE MAGIC", "test the magic", "every search is instant".
- Impacto: riesgo regulatorio por insinuar un uso diagnóstico, expectativas falsas (la app encuentra lo parecido por categoría, no la foto concreta) y asistentes de IA que repiten cifras que no se han medido.
- Opciones: A) ajustar la ficha al documento (cambios de abajo) · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada
- Documento: `docs/definicion-tecnica.md` · "Arquitectura" dice: "TensorFlow Lite […]; en Android, con aceleración por GPU (GpuDelegateV2)".
- Fuente: ficha de App Store dice: "Runs on your phone's hardware (GPU / Neural Engine)". El código lo confirma: `../solopila/lib/services/embedding_service.dart:14-30` solo añade `GpuDelegateV2` si `Platform.isAndroid`; en iOS el intérprete no usa ningún delegado (CPU). No se usa el Neural Engine.
- Impacto: es una afirmación técnica falsa precisamente en la tienda de iOS.
- Opciones: A) quitar "(GPU / Neural Engine)" (propuesto abajo) · B) Anibal revisa el documento
- Esperando decisión.

### 1.1 Cambios en EN (US): actual → nuevo

| # | Texto actual | Texto nuevo | Motivo (brief / definición) |
|---|---|---|---|
| 1 | Tired of losing […] 14,000+ images? Text search doesn't work for hardware`[unión]` blueprints, or receipts. iSIMILAR fixes that. | Tired of losing […] 14,000+ images? *(primera frase sin cambios)* Words can't describe a circuit board or a blueprint very well. iSIMILAR searches by look instead. | Es una comparación que no se puede sostener: Apple Fotos sí encuentra texto en recibos ("Google Fotos y Apple Fotos…" está prohibido). Pilar Encuentra. |
| 2 | Point your camera at any object — or select a saved photo — and our on-device AI instantly digs up the visually similar`[unión]` images hiding in your phone. | Point your camera at any object — or select a saved photo — and our on-device AI digs up the visually similar images hiding in your phone. | Se quita "instantly" ("encuentra cualquier foto al instante"). |
| 3 | No internet required. 100% private. | No internet required. Your photos never leave your phone. | "100% private" se lee como "cero recopilación de datos" (prohibido). Se usa la frase permitida. |
| 4 | THE MAGIC (How it works): | HOW IT WORKS: | "Nada de magia". |
| 5 | On first launch, iSIMILAR indexes your gallery once (a quick one-time scan). After that, every search is instant`[unión]` even with 15,000+ photos. | On first launch, iSIMILAR indexes your gallery once (a quick one-time scan). After that, each search takes under a second. | "instant" y "15,000+" no tienen datos. Se permite "Busca en menos de un segundo". |
| 6 | • Tech Repair: Photograph an open laptop to instantly find the teardown photos you took 4 months ago. | • Tech Repair: Photograph an open laptop to find similar teardown photos from past repairs. | Parecido por categoría, no por instancia. "Al instante" está prohibido. |
| 7 | • Architects/Builders: Snap a picture of a job site and group all related project photos. | • Architects/Builders: Snap a picture of a job site and find similar photos from your projects. | La app no sabe qué es un "proyecto", y "all" promete de más. |
| 8 | • Doctors/Engineers: Photograph X-rays or schematics and instantly locate past scans. | *(se elimina la línea)* | Sanitarios fuera del mensaje (riesgo regulatorio). |
| 9 | • Everyday Users: Find receipts, specific memes, or similar photos without endless scrolling. | • Everyday Users: Find look-alike receipts, repeated memes, and similar photos without endless scrolling. | "Find receipts" y "specific" suenan a búsqueda exacta o por texto; el brief permite "agrupa documentos que se parecen". |
| 10 | • Lightning Fast: Search results in ~50 ms, even with 15,000+ photos. | • Fast: Search results in under a second. | "50 ms" está prohibido (definición técnica, "Medición"). Superlativo. |
| 11 | • 100% Offline AI: Runs on your phone's hardware (GPU / Neural Engine). Your photos never leave your device. | • Offline AI: Runs on your phone, even in airplane mode. Your photos never leave your device. | Neural Engine es falso en iOS (ver contradicción). "Modo avión" es frase permitida. |
| 12 | • Privacy First: No cloud, no uploads, no accounts needed. | • Privacy First: No photo uploads, no cloud storage, no account needed. | La app envía datos técnicos (RevenueCat, Crashlytics). "No cloud, no uploads" sin matiz suena a cero recopilación. |
| 13 | • Smart Cleanup: Batch delete, organize into albums, or export your results instantly. | • Smart Cleanup: Batch delete, organize into albums, or share your results. | La definición técnica dice "compartir", no "exportar". Se quita "instantly". |
| 14 | We give you 5 Free Camera Searches to test the magic. | We give you 5 Free Camera Searches to try it out. | "Nada de magia". |

Sin cambios porque ya cumplen: el titular, "BUILT FOR PROFESSIONALS:", los tres pasos de "How it works", "PRICING (No Hidden Fees):", "Free Forever" (va acotado a buscar y borrar de una en una, como permite el brief), el párrafo de PRO, "No annoying credit systems.", "Stop scrolling. Start finding." y los enlaces legales.

Cambio opcional (no incluido): en "Point it at a motherboard, a document, or a location.", cambiar "a location" por "a place". "Location" puede sugerir búsqueda por ubicación, que la app no hace. Riesgo bajo; tú decides.

### 1.2 Descripción EN completa tras los cambios (referencia; la puntuación de la línea 3 y los saltos de línea pueden no coincidir con App Store Connect)

```
iSIMILAR: The Private Visual Search Engine for Pros

Tired of losing important reference photos in a messy gallery of 14,000+ images? Words can't describe a circuit board or a blueprint very well. iSIMILAR searches by look instead.

Point your camera at any object — or select a saved photo — and our on-device AI digs up the visually similar images hiding in your phone.

No internet required. Your photos never leave your phone.

HOW IT WORKS:

Open the camera inside iSIMILAR (or pick a photo from your gallery).

Point it at a motherboard, a document, or a location.

In under a second, the AI finds the photos that look like it — even ones you took months ago.

On first launch, iSIMILAR indexes your gallery once (a quick one-time scan). After that, each search takes under a second.

BUILT FOR PROFESSIONALS:
• Tech Repair: Photograph an open laptop to find similar teardown photos from past repairs.
• Architects/Builders: Snap a picture of a job site and find similar photos from your projects.
• Everyday Users: Find look-alike receipts, repeated memes, and similar photos without endless scrolling.

KEY FEATURES:
• Fast: Search results in under a second.
• Offline AI: Runs on your phone, even in airplane mode. Your photos never leave your device.
• Privacy First: No photo uploads, no cloud storage, no account needed.
• Smart Cleanup: Batch delete, organize into albums, or share your results.

PRICING (No Hidden Fees):
Searching by existing photos and deleting one-by-one is Free Forever.
We give you 5 Free Camera Searches to try it out.
Need more? Upgrade to iSIMILAR PRO (one simple annual subscription, 7-day free trial) to unlock unlimited Camera Searches and unlimited Batch Actions. No annoying credit systems.

Stop scrolling. Start finding.

Terms & Conditions: https://polar-brian-b09.notion.site/Terms-and-Conditions-for-iSIMILAR-13d88278a02e80e4b5f8d790f9d388f1
Privacy Policy: https://polar-brian-b09.notion.site/Privacy-Policy-for-iSIMILAR-13d88278a02e804aa1a0cbf3b661a05d
```

### 1.3 Cambios en ES: actual → nuevo

Obtenido con `country=es`. **No puedo confirmar** si es la localización "Español (España)" o "Español (México)"; mantengo "recibos", que sirve en los dos.

| # | Texto actual | Texto nuevo |
|---|---|---|
| 1 | La búsqueda por texto no sirve para hardware, planos o recibos. iSIMILAR lo soluciona. | Con palabras cuesta describir una placa o un plano. iSIMILAR busca por parecido visual. |
| 2 | …y nuestra IA en el dispositivo encuentra al instante las imágenes visualmente similares que esconde tu teléfono. | …y nuestra IA en el dispositivo encuentra las imágenes visualmente similares que esconde tu teléfono. |
| 3 | Sin conexión a internet. 100% privado. | Sin conexión a internet. Tus fotos nunca salen del teléfono. |
| 4 | LA MAGIA (Cómo funciona): | CÓMO FUNCIONA: |
| 5 | Después, cada búsqueda es instantánea — incluso con más de 15.000 fotos. | Después, cada búsqueda tarda menos de un segundo. |
| 6 | • Reparación técnica: Fotografía un portátil abierto y encuentra al instante las fotos del desmontaje que tomaste hace 4 meses. | • Reparación técnica: Fotografía un portátil abierto y encuentra fotos parecidas de desmontajes anteriores. |
| 7 | • Arquitectos/Constructores: Haz una foto de una obra y agrupa todas las fotos del proyecto relacionadas. | • Arquitectos/Constructores: Haz una foto de una obra y encuentra fotos parecidas de tus proyectos. |
| 8 | • Médicos/Ingenieros: Fotografía radiografías o esquemas y localiza al instante escaneos anteriores. | *(se elimina la línea)* |
| 9 | • Usuarios cotidianos: Encuentra recibos, memes concretos o fotos parecidas sin hacer scroll sin fin. | • Usuarios cotidianos: Encuentra recibos que se parecen, memes repetidos y fotos parecidas sin hacer scroll sin fin. |
| 10 | • Ultrarrápido: Resultados de búsqueda en ~50 ms, incluso con más de 15.000 fotos. | • Rápido: Resultados de búsqueda en menos de un segundo. |
| 11 | • IA 100% offline: Se ejecuta en el hardware de tu teléfono (GPU / Neural Engine). Tus fotos nunca salen del dispositivo. | • IA sin conexión: Funciona en tu teléfono, incluso en modo avión. Tus fotos nunca salen del dispositivo. |
| 12 | • Privacidad ante todo: Sin nube, sin subidas, sin cuentas. | • Privacidad ante todo: Sin subir fotos, sin guardarlas en la nube, sin cuentas. |
| 13 | • Limpieza inteligente: Borra en lote, organiza en álbumes o exporta tus resultados al instante. | • Limpieza inteligente: Borra en lote, organiza en álbumes o comparte tus resultados. |
| 14 | Te damos 5 búsquedas con cámara gratis para probar la magia. | Te damos 5 búsquedas con cámara gratis para que la pruebes. |

Sin cambios: el titular, "HECHO PARA PROFESIONALES:", los pasos, "PRECIOS (Sin cargos ocultos):", "…es gratis para siempre" (acotado), el párrafo de PRO, "Deja de hacer scroll. Empieza a encontrar." y los enlaces.

### 1.4 Cambios en IT: actual → nuevo

| # | Texto actual | Texto nuevo |
|---|---|---|
| 1 | La ricerca testuale non funziona per hardware, planimetrie o ricevute. iSIMILAR risolve il problema. | Con le parole è difficile descrivere una scheda madre o una planimetria. iSIMILAR cerca per somiglianza visiva. |
| 2 | …e la nostra IA sul dispositivo trova all'istante le immagini visivamente simili nascoste nel tuo telefono. | …e la nostra IA sul dispositivo trova le immagini visivamente simili nascoste nel tuo telefono. |
| 3 | Nessuna connessione internet richiesta. 100% privato. | Nessuna connessione internet richiesta. Le tue foto non lasciano mai il telefono. |
| 4 | LA MAGIA (Come funziona): | COME FUNZIONA: |
| 5 | Dopo, ogni ricerca è istantanea — anche con oltre 15.000 foto. | Dopo, ogni ricerca richiede meno di un secondo. |
| 6 | • Riparazione tecnica: Fotografa un portatile aperto per trovare all'istante le foto dello smontaggio scattate 4 mesi fa. | • Riparazione tecnica: Fotografa un portatile aperto per trovare foto simili di smontaggi precedenti. |
| 7 | • Architetti/Costruttori: Scatta una foto di un cantiere e raggruppa tutte le foto del progetto correlate. | • Architetti/Costruttori: Scatta una foto di un cantiere e trova foto simili dei tuoi progetti. |
| 8 | • Medici/Ingegneri: Fotografa radiografie o schemi e individua all'istante scansioni precedenti. | *(si elimina la riga)* |
| 9 | • Utenti quotidiani: Trova ricevute, meme specifici o foto simili senza scorrere all'infinito. | • Utenti quotidiani: Trova ricevute che si somigliano, meme ripetuti e foto simili senza scorrere all'infinito. |
| 10 | • Fulmineo: Risultati di ricerca in ~50 ms, anche con oltre 15.000 foto. | • Veloce: Risultati di ricerca in meno di un secondo. |
| 11 | • IA 100% offline: Funziona sull'hardware del tuo telefono (GPU / Neural Engine). Le tue foto non lasciano mai il dispositivo. | • IA offline: Funziona sul tuo telefono, anche in modalità aereo. Le tue foto non lasciano mai il dispositivo. |
| 12 | • Privacy prima di tutto: Nessun cloud, nessun upload, nessun account. | • Privacy prima di tutto: Nessuna foto caricata, nessun archivio cloud, nessun account. |
| 13 | • Pulizia intelligente: Elimina in blocco, organizza in album o esporta i risultati all'istante. | • Pulizia intelligente: Elimina in blocco, organizza in album o condividi i risultati. |
| 14 | Ti diamo 5 ricerche con la fotocamera gratuite per provare la magia. | Ti diamo 5 ricerche con la fotocamera gratuite per provarla. |

Sin cambios: el titular, "PENSATO PER I PROFESSIONISTI:", los pasos, "PREZZI (Nessun costo nascosto):", "…è gratis per sempre" (acotado), el párrafo de PRO, "Smetti di scorrere. Inizia a trovare." y los enlaces.

### 1.5 Hipótesis, medición y decisión

- **Hipótesis:** quitar las promesas infladas no baja la conversión de visita a descarga (casi nadie lee la descripción; pesan las capturas) y sí reduce la decepción tras la compra. También evita que ChatGPT repita "50 ms" o el uso médico.
- **Cómo se mide:** la conversión de visita a descarga en App Store Connect (EE. UU., Italia y España por separado), las cancelaciones de prueba y los reembolsos en RevenueCat, y una prueba manual en ChatGPT y Perplexity ("app to find similar photos on iPhone offline") para ver si siguen citando "50 ms" o "X-rays".
- **Cuándo se decide:** 4 semanas después de publicar la versión. **Aviso:** con 4 pagos al mes no habrá diferencia estadística. El cambio se justifica por cumplir el brief y reducir riesgos, no porque se espere un salto medible. No hay nada que probar con una A/B: es corregir errores.
- **Nota de tienda:** la descripción solo se puede cambiar al enviar una versión nueva. Conviene incluirla en el próximo envío junto con las capturas nuevas.

### 1.6 Revisión `tono-de-marca` (descripción corregida)

- Pilares: Encuentra (titular, pasos, perfiles), Ordena (Smart Cleanup y PRO) y Privado (offline, las fotos no salen del teléfono). Cumple.
- Promesas prohibidas: ya no quedan "50 ms", "instant", "magic", "100% private", "exact" ni "15,000+". "Free Forever" va acotado. Cumple.
- Precio y PRO: anual, 7 días de prueba y lote solo en PRO. No se da cifra de precio (la muestra la tienda). Cumple.
- Superlativos: se quita "Lightning Fast" y "Ultrarrápido". Quedan "Smart Cleanup" y "Pulizia intelligente", que son flojos pero no prometen nada. Cumple.
- Veredicto: **apto con cambios** (los de las tablas).

---

## Tarea 2. Respuesta del muro de pago sobre precisión (`faq_a3`)

### 2.1 Texto actual

| Archivo | Clave | Texto actual |
|---|---|---|
| `../solopila/lib/l10n/intl_en.arb:462` | `faq_a3` | Very. The AI analyzes the visual structure of each photo — shapes, textures, patterns — not just colors. A circuit board is a circuit board from any angle. Results in under 1 second. |
| `../solopila/lib/l10n/intl_es.arb:357` | `faq_a3` | Muy precisa. La IA analiza la estructura visual de cada foto — formas, texturas, patrones — no solo colores. Una placa base es una placa base desde cualquier ángulo. Resultados en menos de 1 segundo. |
| `../solopila/lib/l10n/intl_it.arb:357` | `faq_a3` | Molto. L'IA analizza la struttura visiva di ogni foto — forme, texture, pattern — non solo i colori. Una scheda madre è una scheda madre da qualsiasi angolazione. Risultati in meno di 1 secondo. |

⚠️ Contradicción detectada
- Documento: `docs/brief-marketing.md` · "Qué es iSIMILAR" dice: "Funciona mejor con fotos hechas en condiciones parecidas: mismo ángulo, misma luz, mismo fondo. Acierta en torno al 80% de las veces". `docs/definicion-tecnica.md` · "Límites conocidos" dice: "Parecido por categoría, no por instancia".
- Fuente: `../solopila/lib/l10n/intl_en.arb:462` (y `intl_es.arb:357` e `intl_it.arb:357`) dice: "Very. […] A circuit board is a circuit board from any angle."
- Impacto: el muro de pago promete justo lo contrario del límite documentado, en el momento en que se decide la compra. Riesgo de cancelar la prueba o de pedir reembolso.
- Opciones: A) sustituir por el texto de 2.3 · B) Anibal revisa el documento
- Esperando decisión.

### 2.2 Revisión de la propuesta de Anibal

> "Accurate for most photos, around 8 in 10. Works best with photos taken in similar conditions: same angle, light and background."

A favor:
- Es fiel al brief (80% y mismas condiciones) y quita el "from any angle", que es lo grave.
- Es honesta en el muro, que es donde se decide la venta (3 de 4 pagos llegan en los primeros 20 minutos). Ajustar la expectativa antes de pagar reduce los reembolsos.

En contra o mejorable:
1. **"Accurate for most photos, around 8 in 10" repite la idea dos veces** ("most" y "8 in 10") y se lee forzado en inglés. La formulación del brief, "acierta en torno al 80% de las veces", queda más natural como "Right about 8 times out of 10."
2. **Falta el límite que más decepciona al perfil prioritario.** El técnico espera encontrar "la placa de ese cliente" y la app devuelve placas en general (definición técnica: "por categoría, no por instancia"). Si cabe una frase más, esta es la que más evita la decepción.
3. **Se pierde qué compara la app.** La frase actual "shapes, textures, patterns" sí era útil y es verdad (brief: forma, textura, color y composición). Ayuda a entender por qué funciona y no cuesta nada.
4. **Riesgo de dar una cifra:** "8 in 10" sale de un mAP de 0,79 sobre 917 imágenes de prueba, no de las galerías reales. El brief lo autoriza, así que se puede usar. Pero si la destilación a MobileNetV3/384 cambia la precisión, **habrá que actualizar este texto** en la misma versión (lo dice el ROADMAP: no se anuncia nada sin medirlo).
5. **Longitud:** no puedo confirmar cuánto espacio da el muro sin ver la pantalla. El texto actual tiene unos 190 caracteres (EN). Doy una versión completa (unos 215) y una corta (unos 135) por si no cabe.

### 2.3 Texto final propuesto (`faq_a3`)

**Versión recomendada:**

| Idioma | Archivo | `faq_a3` nuevo |
|---|---|---|
| EN | `intl_en.arb:462` | Right about 8 times out of 10. It compares shape, texture, color and composition, so it finds photos that look alike, not one exact photo. Works best with photos taken in similar conditions: same angle, light and background. |
| ES | `intl_es.arb:357` | Acierta unas 8 de cada 10 veces. Compara forma, textura, color y composición: encuentra fotos que se parecen, no una foto exacta. Funciona mejor con fotos hechas en condiciones parecidas: mismo ángulo, misma luz y mismo fondo. |
| IT | `intl_it.arb:357` | È precisa circa 8 volte su 10. Confronta forma, texture, colore e composizione: trova foto che si somigliano, non una foto esatta. Funziona meglio con foto scattate in condizioni simili: stessa angolazione, stessa luce e stesso sfondo. |

**Versión corta (si la recomendada no cabe):**

| Idioma | `faq_a3` corto |
|---|---|
| EN | Right about 8 times out of 10. Works best with photos taken in similar conditions: same angle, light and background. |
| ES | Acierta unas 8 de cada 10 veces. Funciona mejor con fotos hechas en condiciones parecidas: mismo ángulo, misma luz y mismo fondo. |
| IT | È precisa circa 8 volte su 10. Funziona meglio con foto scattate in condizioni simili: stessa angolazione, stessa luce e stesso sfondo. |

Notas de aplicación (en una sesión de `../solopila/`): ninguno de los textos lleva `{}`, así que no rompe el formato ICU. Después hay que regenerar `lib/generated/`.

**Hipótesis y medición:** la respuesta honesta no reduce los pagos y sí reduce las cancelaciones y los reembolsos. Se mide en RevenueCat: conversión del muro a prueba o compra por `paywall_trigger`, cancelaciones de prueba y reembolsos, 4 semanas antes y después de la versión. Mismo aviso: con este volumen la decisión se toma por principio (brief), no por estadística.

### 2.4 Revisión de `faq_q3` y de las respuestas cercanas

| Clave | Texto actual (EN; ES e IT dicen lo mismo) | Valoración | Propuesta |
|---|---|---|---|
| `faq_q3` | How accurate is the search? | Cumple. Nota ES: "¿Qué tan precisa…?" es más de Latinoamérica; en España se diría "¿Cómo de precisa…?". Es menor y opcional. | Sin cambios (ES opcional: "¿Es precisa la búsqueda?", neutro). |
| `faq_a1` | Scanning your full gallery, unlimited searches from saved photos, deleting photos one by one, and your first 5 Camera Searches — completely free. | Coincide con el plan gratuito del brief y de la definición. "completely free" va acotado a esa lista. | Sin cambios. |
| `faq_a2` | Unlimited camera searches + batch delete and move. Organize dozens of photos in one tap, as many times as you want. | Cumple. Es mejorable: el brief y las capturas hablan de "hundreds" ("Delete hundreds at once"). | Opcional: "dozens" → "hundreds" (ES "decenas" → "cientos", IT "decine" → "centinaia"). |
| `faq_a4` | Completely. AI search, batch actions, and albums all work 100% offline. Your photos never leave your device. | Riesgo, no contradicción directa. Comprar o restaurar PRO necesita internet, y **no puedo confirmar** que RevenueCat valide PRO sin conexión en todos los casos. "Completely… 100%" es absoluto. | EN: "Yes. Search, batch actions and albums work offline, even in airplane mode. Your photos never leave your device." / ES: "Sí. La búsqueda, las acciones en lote y los álbumes funcionan sin conexión, incluso en modo avión. Tus fotos nunca salen del dispositivo." / IT: "Sì. Ricerca, azioni in blocco e album funzionano offline, anche in modalità aereo. Le tue foto non lasciano mai il dispositivo." |
| `faq_a5` | You can cancel anytime with one tap in your store settings. You keep PRO access until the end of the year. | **Incorrecto:** se mantiene PRO hasta el final del periodo pagado (o de la prueba), no hasta "el final del año" natural. Un texto engañoso sobre la cancelación es un riesgo de revisión en la tienda y de consumo. No contradice `docs/` de forma literal, pero choca con "suscripción anual con 7 días de prueba" de la definición técnica. Lo paso a `legal-tiendas`. | EN: "Cancel anytime in your App Store or Google Play settings. You keep PRO until the end of the period you've paid for." / ES: "Cancela cuando quieras desde los ajustes de App Store o Google Play. Mantienes PRO hasta el final del periodo pagado." / IT: "Annulla quando vuoi dalle impostazioni di App Store o Google Play. Mantieni PRO fino alla fine del periodo pagato." ("one tap" se quita porque no es verdad: son varios toques). |

Fuera del alcance pero visto de paso (no verificado): en `intl_en.arb:444-446` siguen las claves `all_trial_actions_used` ("All free actions used") y `trial_footer_message` ("…get credits for less than a coffee"), y en `lib/generated/` aparecen `credits_*`. La definición técnica dice que no hay créditos ni "free actions". **No he comprobado si alguna pantalla las sigue mostrando.** Conviene revisarlo en una sesión de `../solopila/` antes de la próxima versión (`checklist-release`).

### 2.5 Revisión `tono-de-marca` (`faq_*` propuestos)

- Pilares: Encuentra (`faq_a3`) y Privado (`faq_a4`). Cumple.
- Sin promesas prohibidas: se quitan "Very", "from any angle", "100%" y "Completely". La cifra de 80% está autorizada por el brief. Cumple.
- Precio: no se menciona. `faq_a5` deja de dar un dato falso sobre el periodo. Cumple.
- Idioma natural en cada mercado, no traducción literal ("Acierta", "È precisa", "Right about"). Cumple.
- Veredicto: **apto con cambios**.

---

## Propuesta para `decisiones/` (solo si Anibal aprueba)

`decisiones/2026-10-22-ficha-y-muro-precision.md`: "La descripción de App Store (EN/ES/IT) y `faq_a3` del muro se alinean con el brief: sin sanitarios, sin 50 ms, sin magia, sin Neural Engine; la precisión se comunica como 'acierta unas 8 de cada 10 veces' y se revisa tras la destilación."
