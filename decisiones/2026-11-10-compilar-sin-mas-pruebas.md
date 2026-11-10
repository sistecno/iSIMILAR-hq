# 2026-11-10 · Compilar sin más pruebas previas

**Decisión (Anibal):** T14, T15 y T16 quedan probados. No se hacen más pruebas antes de
compilar. Se une `fix/T14-T15` a `main`, se sube la versión y se compila.

**Las pruebas que faltaban se hacen sobre la compilación de la tienda** (TestFlight y prueba
interna de Google Play), antes de liberar la versión. Publicación manual en App Store y
gestionada en Google Play, así que nada llega al público sin ese paso:
- 7 días gratis con un usuario nuevo (hoja de compra, PRO al momento, RevenueCat lo marca
  como prueba, al cancelar sigue PRO, al caducar todo pasa a gratis, el botón ya no dice
  "7 días gratis").
- Reinstalar → "Restaurar compras" → vuelve a ser PRO; y qué pasa tras "Restablecer App".

**Por qué:** ya se han hecho muchas pruebas y la compilación de la tienda es la que importa.
**Riesgo:** si falla en la tienda, hay que corregir, compilar y volver a pasar la revisión
(unos días más).

Textos de T10 y T13: revisados con `tono-de-marca`, aptos sin cambios.
