# T10 · Escribir sobre una foto y compartirla (decidido por hq el 2026-11-02)

Para `solopila`. Va en la versión que se está cerrando (Anibal acepta el retraso).
Decisión: `decisiones/2026-11-02-anotar-y-compartir.md`. **No cambia `docs/`** hasta
probar que funciona; por eso no se anuncia en la web, la ficha ni las capturas.

## Por qué
Al compartir desde iSIMILAR (`share_plus`), ni WhatsApp ni Gmail dejan editar la foto
(comprobado por Anibal). Quien encuentra un recuerdo o una foto de trabajo quiere añadir
un mensaje o señalar algo antes de enviarla. La marca de agua hace que cada foto enviada
dé a conocer la app.

## Alcance: lo mínimo, nada más
- **Entrada:** un botón nuevo en `lib/views/widgets/full_image_dialog.dart`, al lado de
  compartir (icono de lápiz). Así sirve desde los resultados y desde el visor de álbumes.
  Solo una foto; no hay edición en lote.
- **Texto:** escribir, mover con el dedo, escalar y rotar con dos dedos, y borrar.
  Tres fuentes **incluidas en la app** (nunca descargadas: la app funciona sin conexión):
  Montserrat (ya está), una manuscrita y una gruesa de estilo meme, ambas con licencia OFL
  (por ejemplo, Caveat y Anton). Cinco colores: blanco, negro, rojo, amarillo y azul. El texto
  lleva un contorno de contraste para que se lea sobre cualquier foto.
- **Corazones y emojis:** desde el teclado del sistema, dentro del texto. No hay stickers.
- **Lápiz:** trazo libre, con los mismos cinco colores y un solo grosor.
- **Deshacer** el último paso, y **cancelar** para salir sin guardar nada.
- **Compartir:** genera la imagen y abre el menú de compartir del sistema.
- **Fuera de alcance:** filtros, recortes, stickers, más fuentes, plantillas y guardar en la
  galería.

## Reglas
1. **No se guarda nada en la galería.** La imagen anotada se escribe en la carpeta temporal,
   se comparte y se borra después (`TempFilesCleaner` ya limpia `tmp`). El original no se
   toca.
2. **Gratis:** 1 foto anotada al día, siempre con marca de agua.
   **PRO:** sin límite y sin marca de agua.
3. **Marca de agua:** el icono de iSIMILAR y el texto "iSIMILAR", abajo a la derecha. Debe ser
   pequeña, semitransparente y bonita, pero legible en la vista previa de WhatsApp, para que
   quien la recibe pueda buscar la app. Se ve en el editor desde el principio (sin sorpresas
   al enviar). Su tamaño es proporcional a la imagen, no a la pantalla.
4. **Contador diario:** en `shared_preferences` (no tocar ObjectBox), por día natural local.
   Cuenta al compartir, no al abrir el editor. Si `ShareResult` dice `dismissed`, no cuenta.
   Que reinstalar o cambiar la hora lo reinicie es aceptable.
5. **Con la foto gratis del día ya usada:** el muro sale **al tocar el lápiz**, antes de
   editar, para que nadie pierda el trabajo hecho. Trigger: `annotate_limit`.
6. **Quitar la marca de agua siendo gratis:** al tocar la marca de agua en el editor sale el
   muro. Trigger: `annotate_watermark`. Si compra, la marca de agua desaparece y sigue editando.
7. **Exportación:** se dibuja sobre la imagen a su resolución real (posiciones guardadas en
   coordenadas relativas, no en píxeles de pantalla), con el lado largo limitado a 4096 px para
   no agotar la memoria en el Mi A3. JPEG de calidad 90, sin metadatos.
8. **Implementación:** se recomienda hacerla a mano (`CustomPainter` + `PictureRecorder`), sin
   una dependencia nueva. Si `solopila` ve un paquete que ahorra mucho trabajo sin meter
   funciones ni permisos de más, lo anota en el buzón antes de usarlo.

## Medición (RevenueCat, que es lo que ya funciona)
- En `AnalyticsService`: `paywallAnnotateLimit = 'annotate_limit'`,
  `paywallAnnotateWatermark = 'annotate_watermark'` y `actionAnnotateShare = 'annotate_share'`.
- Al compartir una foto anotada, llamar a `photoAction(action: actionAnnotateShare, photoCount: 1, …)`.

## Textos (EN / ES / IT)
Pendientes de `tono-de-marca` en hq antes de publicar; se pueden usar ya para programar.

| Clave | ES | EN | IT |
|---|---|---|---|
| `annotate_button` | Escribir | Write | Scrivi |
| `annotate_text` | Texto | Text | Testo |
| `annotate_draw` | Lápiz | Pen | Penna |
| `annotate_undo` | Deshacer | Undo | Annulla |
| `annotate_share` | Compartir | Share | Condividi |
| `annotate_free_hint` | Gratis: 1 foto al día con marca de agua | Free: 1 photo a day with watermark | Gratis: 1 foto al giorno con filigrana |
| `paywall_title_annotate_limit` | Escribe sobre todas las fotos que quieras, sin marca de agua | Write on as many photos as you like, no watermark | Scrivi su tutte le foto che vuoi, senza filigrana |
| `paywall_title_annotate_watermark` | Comparte tus fotos sin marca de agua | Share your photos without a watermark | Condividi le tue foto senza filigrana |

El muro cambia el titular según el trigger, igual que con las acciones en lote. El resto del
muro no cambia en esta versión.

## Pruebas antes de dar por hecho (iPhone y Mi A3)
- [ ] Compartir anotada a WhatsApp, Gmail y Telegram: se ve el texto, el trazo y la marca de agua.
- [ ] Foto vertical, foto horizontal, HEIC (iOS) y foto grande (48 MP o la mayor disponible).
- [ ] Emoji ❤️ en el texto: aparece igual en la imagen enviada.
- [ ] El teclado no tapa el texto que se está escribiendo.
- [ ] Gratis: la primera del día sale con marca de agua; la segunda abre el muro (`annotate_limit`).
- [ ] Cancelar el menú de compartir no gasta la foto del día (donde `ShareResult` lo indique).
- [ ] Tocar la marca de agua abre el muro (`annotate_watermark`). Con PRO no hay marca ni límite.
- [ ] La galería no tiene fotos nuevas y `tmp` queda limpio.
- [ ] Modo avión: todo funciona.
- [ ] RevenueCat recibe `paywall_trigger` con los dos valores nuevos.

Al terminar: informe en `docs/PARA-HQ-DE-SOLOPILA.md` con los commits y lo que no se haya
podido probar.

## Ajustes tras la primera prueba de Anibal (2026-11-02)
Probado por Anibal en el Mi A3: el texto, las fuentes, el ❤️ y el lápiz funcionan, y en modo
gratis el límite de 1 al día lleva al muro. Falta comprobarlo en RevenueCat (ver más abajo).

Respuesta de hq al informe de `solopila` (16:40):
1. **El lápiz tiene que verse sin abrir "Detalles".** Si nadie lo encuentra, la medición
   a 30 días no sirve. Ponlo a la vista en el visor de la foto. Compartir se queda donde está.
   Tú eliges el sitio exacto; muestra a Anibal una captura antes de unir a `main`.
2. **Al cancelar, pedir confirmación solo si hay cambios** (texto o trazo). Sin cambios, se
   sale directamente. Para "Cancelar" se usa la clave que ya exista.

| Clave | ES | EN | IT |
|---|---|---|---|
| `annotate_discard_title` | ¿Salir sin compartir? | Leave without sharing? | Uscire senza condividere? |
| `annotate_discard_body` | Se perderá lo que has escrito y dibujado. | What you wrote and drew will be lost. | Quello che hai scritto e disegnato andrà perso. |
| `annotate_discard_confirm` | Salir | Leave | Esci |

3. **Marca de agua:** no se cambia hasta verla. Anibal envía por WhatsApp una foto vertical y
   otra horizontal y manda una captura de la vista previa del chat. Si no se lee el nombre,
   se ajusta el tamaño.
4. **RevenueCat:** el código llama a `setPaywallTrigger` igual que en los lotes. Antes de
   tocar nada, hay que confirmar en el panel que el problema no es de visualización
   (datos de prueba ocultos o atributos que aún no se han sincronizado).
