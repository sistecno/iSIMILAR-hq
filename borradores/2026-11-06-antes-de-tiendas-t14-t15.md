# T14 y T15 · Antes de enviar a tiendas (decidido por hq el 2026-11-06)

Para `solopila`. Decisión: `decisiones/2026-11-06-antes-de-tiendas.md`.
**Orden:** primero unir `feature/T10-anotar` a `main` (OK dado el 2026-11-06). Después, rama
nueva `fix/T14-T15` a partir de `main`. No cambia `docs/`.

## T14 · El estado PRO tiene que ser el mismo en toda la app

**Problema (visto por `solopila` el 2026-11-06):** con una suscripción de prueba caducada, el
muro sale bien, pero Ajustes sigue diciendo "ilimitado".
- `isPremium()` consulta RevenueCat en vivo. Lo usan el editor y las acciones en lote.
- `isPremiumSync` (`_isPremiumCached`, `home_view_model.dart:953`) se guarda al abrir la app y
  no se actualiza. Lo usan:
  - `premium_status_card.dart:19` (Ajustes);
  - `image_selection_view.dart:202, 385, 700` (botón PRO y contador de la pantalla principal);
  - `premium_offer_sheet.dart:109`.

**Lo que se pide:**
1. **Una sola fuente de verdad.** `_isPremiumCached` se actualiza con
   `Purchases.addCustomerInfoUpdateListener`, al volver la app del fondo y después de comprar o
   restaurar. Cada cambio llama a `notifyListeners()`, para que Ajustes, el contador y el botón
   PRO cambien solos.
2. **Que no cambie nada para quien paga.** Sin conexión, RevenueCat usa su caché: un PRO
   activo no puede pasar a gratis por estar en modo avión.
3. **No tocar** los precios, el muro ni la compra.

**Pruebas:**
- [ ] Suscripción de prueba caducada (iOS y Android): Ajustes, el contador de la cámara y el
      botón PRO pasan a gratis sin reinstalar. Como mucho, al volver la app del fondo.
- [ ] Comprar y restaurar: todo pasa a PRO al momento.
- [ ] PRO activo en modo avión: sigue siendo PRO en toda la app.
- [ ] El editor (marca de agua y límite) sigue el mismo estado que Ajustes.

## T15 · Marca de agua visible en la vista previa del chat de WhatsApp

**Objetivo:** que quien recibe la foto vea "iSIMILAR" sin abrirla. Si no se ve, la medición de
descargas desde WhatsApp no sirve.

**Paso 1 · Anibal elige con la prueba real (10 minutos):**
1. Pasar al móvil las 6 variantes de `~/Downloads/T10-marca-agua/` (A, B y C, en vertical y
   en horizontal), por ejemplo con AirDrop.
2. Enviarlas por WhatsApp a un chat propio o de confianza.
3. Hacer una captura del chat (la vista previa, sin abrir las fotos) y pasarla a hq.
4. Se elige la posición que se lea en vertical **y** en horizontal. Si ninguna se lee en las
   dos, `solopila` propone una variante más (por ejemplo, arriba a la izquierda) y se repite.

**Paso 2 · `solopila` aplica la posición elegida:**
- Un solo cambio de posición en el dibujo de la marca de agua. Mismo tamaño, mismo estilo y la
  misma zona para tocar y abrir el muro (`annotate_watermark`) en el editor.
- Probar: foto vertical y horizontal por WhatsApp (captura de la vista previa del chat), y que
  tocar la marca en el editor siga abriendo el muro.

Al terminar T14 y T15: informe en `docs/PARA-HQ-DE-SOLOPILA.md` con los commits.

## Decisiones de hq del 2026-11-09 (buzón de `solopila`, 12:53–13:56)

### T15 · Posición elegida: B (abajo a la izquierda)
Prueba real enviada sin texto desde el iPhone y vista en el chat del iPhone y del Mi A3: B se
lee entera en vertical y en horizontal, y es la que menos tapa la foto. A queda tapada por la
hora; C se lee, pero tapa más. Aplicar B en `fix/T14-T15`: solo cambia la posición (mismo
tamaño, mismo estilo y la misma zona para tocar y abrir el muro).

### T16 · Carpetas nuevas en Android: entran marcadas (opción A, en esta versión)
Se guardan las carpetas **desmarcadas**, no las marcadas, con una conversión única para quien ya
tiene una lista guardada. Se hace en `fix/T14-T15`. No cambia el esquema de ObjectBox
(`ConfigEntity`) ni hay textos nuevos. iOS no cambia.
Pruebas en el Mi A3, además de las tres propuestas por `solopila`:
- [ ] Una carpeta nueva entra marcada y se escanea con "Buscar fotos nuevas".
- [ ] Una carpeta desmarcada por el usuario sigue desmarcada.
- [ ] Quien tenía una lista guardada conserva su elección después de la conversión.
- [ ] La conversión ocurre una sola vez: abrir la app dos veces no cambia nada.
- [ ] Instalación nueva: todas las carpetas marcadas, igual que hoy.
- [ ] "Reset App" deja la elección como en una instalación nueva.
- [ ] Una carpeta que desaparece (se borra) no da error y no rompe la lista.
