# Botón de pago cuando no llega el precio (2026-10-30)

## Decisión: A
- El botón de compra del muro está siempre activo. Principio: el botón siempre funciona.
- Si el precio no ha llegado de la tienda: no se muestra ningún precio escrito a mano;
  se muestra carga o "No se pudo cargar el precio" (EN/ES/IT).
- Al pulsar sin producto cargado: spinner y nueva petición. Si llega, el muro muestra el
  precio real y la prueba, y se abre la hoja nativa de Apple o Google. Si no llega,
  mensaje claro "Sin conexión con la tienda, inténtalo de nuevo".
- Mientras no se sepa si hay prueba, el botón no dice "Desbloquear todo" (texto neutro).

## Por qué
- Un fallo momentáneo de conexión no debe costar la venta.
- El código ya funcionaba así (cada toque vuelve a pedir el producto) y ha pasado las
  revisiones. Los problemas reales eran el precio de respaldo `$12.99` (precio falso,
  en dólares y distinto de los 15,99 de Google Play) y el fallo silencioso: el `Exception`
  de `premium_service.dart:61` no lo captura `_purchase`, que solo atrapa `PlatformException`.
- Se corrige la instrucción de T4 ("no permitir comprar"), que fue un error de hq.

## Riesgo aceptado
- Norma 3.1.2 de Apple: en el caso de reintento, el usuario ve el precio en la hoja nativa
  y no antes en el muro. Riesgo bajo: solo ocurre si falla la carga.
- Descartadas: B (primer toque solo recarga, segundo compra: un paso más justo tras un
  fallo) y C (botón desactivado: contradice el principio).

## Regla de proceso
- Las sesiones de `solopila/` y de la web no crean decisiones: las piden a hq, que las
  escribe y guarda en `decisiones/`.
