# Antes de enviar a tiendas: estado PRO, marca de agua y permiso de fotos (2026-11-06)

## Contexto
Con T10 y T13 probados, `solopila` señaló dos problemas que ya existían (buzón 2026-11-06 12:36),
y la marca de agua en posición A no se ve en la vista previa del chat de WhatsApp.

## Decisión (Anibal)
1. **T14:** se arregla en esta versión que, con PRO caducado, Ajustes siga diciendo "ilimitado".
   Una sola fuente de verdad para el estado PRO.
2. **T15:** la marca de agua se mueve en esta versión a una posición que se vea en la vista
   previa del chat de WhatsApp, elegida con una prueba real. Sustituye a "A en esta versión",
   decidido antes el mismo día.
3. **Acceso completo a las fotos al arrancar:** se mantiene y no se revisa. La app no tiene
   sentido sin acceso a la galería, el usuario lo sabe por la solicitud de permiso y todas las
   versiones han pasado la revisión de Apple.

## Alternativas descartadas
- Dejar T14 para más adelante: un usuario (o un revisor de Apple) vería PRO sin tenerlo.
- Mantener la marca en A: quien recibe la foto no ve la marca sin abrirla, y la revisión a
  30 días de las descargas desde WhatsApp no diría nada.
- Admitir acceso limitado a las fotos: buscar en una galería parcial daría resultados pobres.

## Cómo se revisará
- T14: con las pruebas de la especificación, antes de enviar a tiendas.
- T15: en la revisión de T10 a los 30 días, con las descargas desde WhatsApp.
- Permiso de fotos: solo se vuelve a mirar si una tienda rechaza la app por esto.

Especificación: `borradores/2026-11-06-antes-de-tiendas-t14-t15.md`.
