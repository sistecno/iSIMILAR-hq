# Entradas al muro desde la pantalla principal · Restaurar sin compras (2026-10-30)

## T4h: el muro se abre desde la pantalla principal
- Motivo: un posible cliente no encontró cómo comprar. Hoy el muro solo se abre al chocar
  con un límite (cámara, lote) o desde Ajustes; quien solo busca en la galería nunca lo ve.
  Dato propio: 3 de los 4 pagos llegaron en los primeros 20 minutos (`guia-estrategica.md`).
- Para usuarios sin PRO:
  - El contador de búsquedas con cámara abre el muro, con la línea "Ilimitadas con PRO ›".
  - Botón "PRO" con corona, fijo en la barra superior (solo icono si no cabe).
- Medición: `paywall_trigger` = `home_counter` y `home_appbar`.
- Sin ventanas emergentes ni avisos automáticos: solo puntos de entrada visibles.
- `docs/definicion-tecnica.md` actualizado con autorización de Anibal (commit 3cb298e).
- Revisar en RevenueCat tras la publicación cuántas aperturas y compras llegan por estas
  dos entradas.

## T4i: Restaurar compras sin compras que restaurar
- Si la restauración no encuentra compras, el muro queda abierto y se avisa:
  "No encontramos compras para restaurar". Antes se cerraba sin aviso.
- Motivo: no hay fallos silenciosos (mismo principio que
  `2026-10-30-boton-pago-sin-precio.md`) y el revisor de Apple suele probar este botón.
- Entra en esta versión, con commit propio después de T4.

Instrucciones completas: `borradores/2026-10-22-instrucciones-app.md` (T4h, T4i).
