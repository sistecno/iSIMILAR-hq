# Escribir sobre una foto y compartirla (2026-11-02)

## Contexto
- Al compartir desde iSIMILAR, ni WhatsApp ni Gmail dejan editar la foto (comprobado por
  Anibal). Quien encuentra un recuerdo olvidado o una foto de trabajo no puede añadirle un
  mensaje ni señalar algo antes de enviarla.
- La retención es el problema principal: 19 % vuelve tras el primer día y 6 % tras 30
  (`docs/guia-estrategica.md`). WhatsApp ya trajo 8 descargas solo con enlaces compartidos.
- Relacionada: `borradores/2026-10-24-idea-recuerdos.md` (iSIMILAR saca recuerdos olvidados).

## Decisión (Anibal)
- Editor mínimo en la vista de una foto: texto (pocas fuentes incluidas), lápiz, emojis por
  teclado, deshacer y compartir. Sin stickers, filtros ni recortes.
- No se guarda nada en la galería: solo se comparte.
- Gratis: 1 foto anotada al día, siempre con marca de agua. PRO: sin límite y sin marca.
- Va en la versión que se está cerrando, aunque la retrase.
- **`docs/` no se cambia hasta probar que funciona.** Excepción consciente: mientras tanto, la
  app tiene una ventaja de PRO que el brief no recoge. No se anuncia en la web, la ficha ni las
  capturas hasta actualizar `docs/`.
- Especificación para `solopila`: `borradores/2026-11-02-anotar-y-compartir.md` (T10).

## Alternativas descartadas
- No hacerlo y confiar en el editor de WhatsApp: no aparece al compartir desde la app.
- Solo un vídeo de contenido: no resuelve el hueco del producto.
- Marca de agua opcional para los usuarios gratis: Anibal quiere que siempre salga; quitarla es PRO.

## Cómo se revisará
A los 30 días de publicar la versión:
- Pagos en RevenueCat con `paywall_trigger` = `annotate_limit` o `annotate_watermark`,
  frente a los demás motivos.
- Descargas desde WhatsApp y otras apps en App Store Connect, frente a las 8 de antes.
- Opiniones y reseñas que hablen de la marca de agua.

Si funciona, se propone a Anibal el texto exacto para el brief (Precio, pilares y "Lo que no
es") y la definición técnica. Si nadie paga y no suben las descargas, se revisa el límite o la
marca de agua antes de tocar `docs/`.
