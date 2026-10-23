# Términos de uso v3.1: precio sin importe fijo y planes actualizados

Autor: agente `legal-tiendas` · 2026-10-23 · Estado: propuesta, pendiente de decisión de Anibal.
Base: textos publicados en `solopila_landingPAGE/astro/src/legal/{en,es,it}/terms.md` (v3).
No soy abogado. Ver al final qué conviene que revise uno.

Cómo aplicarlo: en cada archivo, buscar el "Texto actual" (literal, con sus saltos de
línea) y sustituirlo por el "Texto nuevo". No se tocan los marcadores (`[FECHA]`,
`[NOMBRE]`, etc.) ni `datos.json`. Solo cambian los 3 `terms.md`. `privacy.md` y
`delete-data.md` no cambian (ver apartado D).

---

## A. Cambio 1 · Apartado 4 (planes)

Motivo: brief ("Precio y cómo comunicarlo") y definición técnica ("Modelo comercial en el
código"): en Gratis también se mueve a un álbum y se comparte de una en una; en PRO, el
lote incluye compartir.

### en/terms.md

Texto actual:
```
- Deleting photos one at a time.
```
Texto nuevo:
```
- Deleting, moving to an album or sharing photos one at a time.
```

Texto actual:
```
- Batch actions: deleting or moving many photos at once.
```
Texto nuevo:
```
- Batch actions: deleting, moving to an album or sharing many photos at once.
```

### es/terms.md

Texto actual:
```
- Borrado de fotos de una en una.
```
Texto nuevo:
```
- Borrar, mover a un álbum o compartir fotos de una en una.
```

Texto actual:
```
- Acciones en lote: borrar o mover muchas fotos de una vez.
```
Texto nuevo:
```
- Acciones en lote: borrar, mover a un álbum o compartir muchas fotos de una vez.
```

### it/terms.md

Texto actual:
```
- Eliminazione delle foto una alla volta.
```
Texto nuevo:
```
- Eliminare, spostare in un album o condividere le foto una alla volta.
```

Texto actual:
```
- Azioni multiple: eliminare o spostare molte foto in una volta.
```
Texto nuevo:
```
- Azioni multiple: eliminare, spostare in un album o condividere molte foto in una volta.
```

Nota: "Unlimited searches from photos saved on your phone" ya equivale a "búsquedas
ilimitadas desde fotos guardadas" del brief; no se toca.

---

## B. Cambio 2 · Apartado 5, viñeta "Precio" (sin importes fijos)

Motivo: hoy las tiendas no coinciden (11,99 USD en App Store EE. UU., 15,99 € en Google
Play Italia), así que los términos publicados dan un precio que no es el que se cobra en
Italia. Un precio contractual erróneo es el riesgo principal: es información
precontractual incorrecta para el consumidor (Directiva 2011/83/UE, art. 6.1.e; Codice
del Consumo, art. 49) y una práctica engañosa sobre el precio (Directiva 2005/29/CE,
art. 6.1.d). Decisión de Anibal (2026-10-23): ningún precio fijo fuera de la tienda.

Por qué sigue siendo válida sin importe:
- UE: lo que se exige es que el consumidor conozca el precio total con impuestos antes
  de quedar obligado y justo antes de pagar (Directiva 2011/83/UE, art. 8.2). Eso lo
  cumplen el muro de pago (precio leído de la tienda) y la pantalla de confirmación de
  Apple y Google. Los términos solo tienen que remitir a ese precio y decir que es el
  que se acepta.
- Apple, guía 3.1.2(c): "Before asking a customer to subscribe, you should clearly
  describe what the user will get for the price" y remite al Schedule 2 del Apple
  Developer Program License Agreement. Se cumple en el muro de pago, no en los términos.
  Apple no exige el importe en los términos.
- Google Play (developer.android.com/google/play/billing/price-changes): las subidas de
  precio son por defecto "opt-in": el usuario debe aceptarlas antes del primer cobro o la
  suscripción se cancela al renovar; Google avisa 30 días antes. En algunos países hay
  subidas "opt-out" con aviso de 30 o 60 días y aviso obligatorio dentro de la app.
  Apple tiene un sistema parecido (aviso previo y consentimiento salvo subidas pequeñas
  dentro de sus límites); sin verificar en esta sesión en la página oficial de Apple
  ("Managing prices"), conviene comprobarlo antes de la primera subida.
- Se añade que el precio puede variar entre tiendas: es la situación real hoy y evita
  que la diferencia App Store / Google Play se lea como engaño.

### en/terms.md

Texto actual:
```
- Price: 12 € per year in the euro area and 11.99 USD per year in the United States; in
  other countries, the equivalent price set by the App Store or Google Play. The exact
  price, in your currency and with any taxes that apply, is shown in the app and in the
  store's confirmation screen before you pay.
```
Texto nuevo:
```
- Price: the price depends on your country and on the store (App Store or Google Play),
  and may differ between stores. The exact price, in your currency and with any taxes
  that apply, is shown in the app and in the store's confirmation screen before you pay.
  That is the price you agree to when you subscribe.
```

### es/terms.md

Texto actual:
```
- Precio: 12 € al año en la zona euro y 11,99 USD al año en Estados Unidos; en otros
  países, el equivalente que fija la App Store o Google Play. El precio exacto, en tu
  moneda y con los impuestos aplicables, se muestra en la app y en la pantalla de
  confirmación de la tienda antes de pagar.
```
Texto nuevo:
```
- Precio: depende de tu país y de la tienda (App Store o Google Play), y puede ser
  distinto en cada tienda. El precio exacto, en tu moneda y con los impuestos aplicables,
  se muestra en la app y en la pantalla de confirmación de la tienda antes de pagar. Ese
  es el precio que aceptas al suscribirte.
```

### it/terms.md

Texto actual:
```
- Prezzo: 12 € all'anno nell'area euro e 11,99 USD all'anno negli Stati Uniti; negli
  altri paesi, l'equivalente stabilito dall'App Store o da Google Play. Il prezzo esatto,
  nella tua valuta e con le eventuali imposte, è mostrato nell'app e nella schermata di
  conferma dello store prima del pagamento.
```
Texto nuevo:
```
- Prezzo: dipende dal tuo paese e dallo store (App Store o Google Play) e può essere
  diverso da uno store all'altro. Il prezzo esatto, nella tua valuta e con le eventuali
  imposte, è mostrato nell'app e nella schermata di conferma dello store prima del
  pagamento. È il prezzo che accetti quando ti abboni.
```

---

## C. Cambio 3 · Apartado 5, viñeta "Renovación" (aviso de cambio de precio)

Motivo: sin un importe escrito, la protección del usuario ante una subida tiene que
quedar explícita: aviso previo y, si no acepta cuando la tienda lo exige, la suscripción
no se renueva (así funciona el "opt-in" de Google Play). El resto de la viñeta no cambia.

### en/terms.md

Texto actual:
```
  you cancel before the current period ends. If the price changes, the store will tell
  you in advance and, where required, ask for your consent.
```
Texto nuevo:
```
  you cancel before the current period ends. If the price goes up, you will be told in
  advance by the store and, where the law or the store's rules require it, asked to
  accept the new price; if you do not accept it, the subscription will not renew.
```

### es/terms.md

Texto actual:
```
  que la canceles antes de que termine el periodo en curso. Si el precio cambia, la tienda
  te avisará antes y, cuando sea obligatorio, te pedirá tu conformidad.
```
Texto nuevo:
```
  que la canceles antes de que termine el periodo en curso. Si el precio sube, la tienda
  te avisará antes y, cuando la ley o las normas de la tienda lo exijan, te pedirá que
  aceptes el nuevo precio; si no lo aceptas, la suscripción no se renovará.
```

### it/terms.md

Texto actual:
```
  annullamento prima della fine del periodo in corso. Se il prezzo cambia, lo store ti
  avviserà prima e, quando richiesto, ti chiederà il consenso.
```
Texto nuevo:
```
  annullamento prima della fine del periodo in corso. Se il prezzo aumenta, lo store ti
  avviserà prima e, quando la legge o le regole dello store lo richiedono, ti chiederà di
  accettare il nuovo prezzo; se non lo accetti, l'abbonamento non si rinnoverà.
```

No se cambia nada más del apartado 5: renovación automática, prueba de 7 días,
cancelación 24 h antes, cobro por Apple/Google, cómo cancelar y "Restaurar compras" ya
cumplen y coinciden con los docs.

---

## D. Pago único: ¿dejar la puerta abierta ahora?

Recomendación: **no**. Mantener los términos solo con la suscripción y publicar una v3.2
cuando el pago único exista de verdad.

- Los términos describen lo que se vende. Hoy la definición técnica dice "El único
  producto es una suscripción anual". Escribir ya "o un pago único" describiría un
  producto que no existe y contradice el documento (ver contradicción 3).
- Una cláusula genérica ("PRO puede ofrecerse en distintas modalidades") no basta para
  el pago único: hay que decir qué es exactamente (sin renovación ni cancelación;
  duración: mientras la app se mantenga y esté disponible en la tienda; si se transfiere
  entre plataformas o no; qué pasa si se retira la app; si quien ya tiene suscripción
  puede pasarse y cómo se cancela la suscripción, que no se cancela sola). Esas
  respuestas dependen de decisiones de producto que aún no hay.
- Coste de esperar: bajo. Con la cláusula de precio sin importes (cambio B), añadir el
  pago único será añadir un subapartado nuevo en el apartado 5 y una frase en el 4, no
  reescribir. Además, ampliar la oferta no perjudica a nadie, así que no exigirá aviso
  en la app (apartado 12).
- Ojo con el nombre: si se llama "de por vida" / "lifetime", Apple y la normativa de
  consumo lo leen como promesa; hay que definir "vida" (la de la app, no la del usuario).

---

## E. Revisión de privacy.md y delete-data.md

Ninguno menciona precio ni la lista de funciones Gratis/PRO: **no necesitan cambios por
este motivo.** Hallazgos colaterales (se reportan, no se corrigen aquí):

| Requisito | Estado | Evidencia | Acción |
|---|---|---|---|
| Lista de `paywall_trigger` en privacy 5.2 | cumple hoy | privacy 5.2 lista cámara, borrar en lote, mover en lote, Ajustes = `analytics_service.dart:31-34` | Cuando se añada `batch_share` (pendiente en la definición técnica), actualizar privacy 5.2 en los 3 idiomas antes de publicar esa versión |
| Forma de oponerse (Crashlytics, atributos de medición) | no coincide con docs | privacy 5.2 y 5.3: "email us"; definición técnica, "Consentimiento": interruptor en Ajustes "Compartir datos técnicos…"; en `solopila/lib` no hay `setCrashlyticsCollectionEnabled` ni el interruptor | Contradicción 2 |
| "Undoes the albums created in the app" (delete-data 1) | sin verificar | No lo he comprobado en el código | Comprobar qué hace Reset App con los álbumes |
| Precio / funciones en privacy y delete-data | cumple | Sin menciones | Ninguna |

---

## F. Otros puntos de los términos

- Apartado 3 dice "works on your phone, without an internet connection". Es cierto para
  la búsqueda, pero comprar o restaurar PRO necesita conexión (decisión
  `2026-10-22-ficha-y-muro.md`, faq_a4). Riesgo bajo; no lo cambio. Si Anibal quiere,
  añadir: "Buying or restoring PRO needs a connection." (ES: "Comprar o restaurar PRO
  necesita conexión." IT: "Per acquistare o ripristinare PRO serve una connessione.").
- El resto (apartados 1-3, 6-14) es coherente con el brief y la definición técnica.

---

## G. Fecha y aviso a los usuarios

- **Fecha "Última actualización":** sale de `datos.json` (`FECHA`) y vale para los 3
  documentos a la vez. Ya es 23 de octubre de 2026. Si v3.1 se publica hoy, no hace
  falta cambiarla. Si se publica otro día, cambiar `FECHA` cambia también la fecha de
  privacy y delete-data aunque no hayan cambiado: es inexacto pero inofensivo. La
  alternativa (una fecha por documento) exige tocar la compilación: decisión de Anibal.
- **Aviso a los usuarios: no hace falta.** El apartado 12 obliga a avisar en la app solo
  de cambios importantes. Ninguno perjudica al usuario: se quita un importe (el precio
  real siempre lo fija la tienda antes de pagar), Gratis gana funciones descritas y la
  protección ante subidas se hace más explícita. Además, v3 lleva un día publicada.
  Excepción: si Anibal decide que compartir en lote pasa a ser de PRO en la app y hoy es
  gratis (contradicción 1), eso sí quita algo a usuarios gratuitos; conviene mencionarlo
  en las notas de la versión de la app que lo active.

---

## H. Contradicciones

⚠️ Contradicción detectada
- Documento: `docs/definicion-tecnica.md` · "Modelo comercial en el código" y brief
  · "Precio y cómo comunicarlo" dicen: compartir muchas fotos de una vez es de PRO; "las
  acciones en lote son siempre de PRO".
- Fuente: `solopila/lib/views/widgets/album_detail_sheet.dart:72-87` (`_shareSelected`)
  comparte las fotos seleccionadas sin llamar a `canPerformBatchAction()` ni abrir el
  muro (`paywallShown: false`), a diferencia de mover y borrar en el mismo archivo.
- Impacto: los términos v3.1 dirán que compartir en lote es de PRO y la app lo da gratis
  en el visor de álbumes. No es un riesgo legal para el usuario (recibe más), pero los
  términos no describen la app real y el atributo `batch_share` sigue sin existir.
- Opciones: A) ajustar el código al documento (bloquear compartir en lote y añadir
  `batch_share`) · B) Anibal revisa el documento
- Esperando decisión.

⚠️ Contradicción detectada
- Documento: `docs/definicion-tecnica.md` · "Datos y privacidad", "Consentimiento" dice:
  interruptor en Ajustes "Compartir datos técnicos para mejorar la app", activado por
  defecto, que desactiva Crashlytics, los atributos de medición y la pregunta tras la
  compra.
- Fuente: `privacy.md` 5.2 y 5.3 (EN/ES/IT) dicen que para oponerse hay que escribir un
  email; en `solopila/lib` no aparece el interruptor ni `setCrashlyticsCollectionEnabled`.
- Impacto: la política coincide con el código, no con el documento. Cuando el
  interruptor exista, la política tendrá que explicarlo; si nunca se hace, el derecho de
  oposición por email es válido pero más débil frente al interés legítimo (art. 21 RGPD).
- Opciones: A) ajustar el código al documento (y después la política) · B) Anibal revisa
  el documento
- Esperando decisión.

⚠️ Contradicción detectada
- Documento: `docs/brief-marketing.md` · "Precio y cómo comunicarlo" y
  `docs/definicion-tecnica.md` · "Modelo comercial" dicen: PRO, 12 € al año en la zona
  euro (11,99 USD en EE. UU.); "El precio debe ser el mismo en la app, la ficha de la
  tienda, la web y cualquier material"; "El único producto es una suscripción anual".
- Fuente: Google Play Italia cobra 15,99 € (dato de Anibal, no verificado por mí); la
  decisión del 2026-10-23 quita el precio de la web y, con esta propuesta, de los
  términos; Anibal prevé probar un pago único.
- Impacto: los términos v3.1 no contradicen los docs (no dan importe), pero la tienda sí.
  Mientras Google Play Italia cobre 15,99 €, cualquier material que repita "12 €" sería
  información de precio incorrecta. El pago único no puede aparecer en ningún texto
  legal ni comercial mientras los docs digan que no existe.
- Opciones: A) ajustar la tienda a los docs (unificar a 12 €) · B) Anibal revisa los
  documentos (precio y, cuando toque, el pago único)
- Esperando decisión.

---

## Qué debería revisar un abogado

La cláusula de precio sin importe con remisión a la tienda (B) y la redacción de la
subida de precio (C), sobre todo para Italia (Codice del Consumo, arts. 33-35 sobre
cláusulas que permiten al profesional cambiar el precio) antes de la primera subida
real.

Fuentes consultadas hoy: developer.apple.com/app-store/review/guidelines (3.1.2(a) y
(c)); developer.android.com/google/play/billing/price-changes.
