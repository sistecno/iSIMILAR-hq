# 2026-10-22 · Ficha de App Store y textos del muro de pago

Decidido por Anibal. Propuesta de base: `borradores/2026-10-22-ficha-y-muro.md` (growth).

## Ficha de App Store
- La descripción (EN, ES, IT) se alinea con el brief: sin sanitarios ni radiografías,
  sin "~50 ms", sin "magic", sin "instantly" ni "Lightning Fast".
- Se quita "GPU / Neural Engine" (contradicción 16): en iOS el modelo no usa GPU
  (`solopila/lib/services/embedding_service.dart:14-30`).
- Se aplican solo los cambios "actual → nuevo" del borrador sobre el texto de App Store
  Connect, no la descripción completa reconstruida. Va en el próximo envío de versión.
- La ficha ES es la de España. Se creará una ficha para México (pendiente).

## Muro de pago
- `faq_a3` (precisión): "acierta unas 8 de cada 10 veces", fotos que se parecen y no una
  foto exacta, mejor en condiciones parecidas. Hay dos versiones (larga y corta) en EN, ES
  e IT; se elige durante el desarrollo según el espacio disponible. Se revisa tras la
  destilación si cambia la precisión.
- `faq_a4` (sin conexión, contradicción 18): se centra en lo que Anibal confirma: la
  búsqueda de fotos parecidas funciona sin internet, incluso en modo avión. Comprar o
  restaurar PRO necesita conexión.
- `faq_a5` (cancelación, contradicción 17): el botón de la app abre la gestión de
  suscripciones de la tienda, que se encarga de cancelar. PRO se mantiene hasta el final
  del periodo pagado, no hasta el final del año. Texto final: pendiente de `legal-tiendas`.
- Contradicción 19: la interfaz no muestra créditos. Las claves `all_trial_actions_used` y
  `trial_footer_message` de los `.arb` no se usan en el código (0 referencias); se pueden
  borrar como limpieza, sin urgencia.
