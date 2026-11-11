# Pendientes de iSIMILAR

Actualizado: 2026-11-10. Marca con [x] lo hecho.
Buzones leídos hasta: `solopila` — 2026-11-10 21:24 (T14–T16 probados, bc0765f) · web — (aún vacío).

## 2026-11-10 noche · Compilar (`decisiones/2026-11-10-compilar-sin-mas-pruebas.md`)
- [ ] `solopila`: unir `fix/T14-T15` a `main`, subir versión y compilar. Sin más pruebas antes.
- [ ] Capturas (Anibal) → revisión de hq → encargo de los marcos y textos de la ficha.
      2026-11-11: muro (captura 6) revisado. ES y EN válidas. IT, rehacer: los títulos de las
      tarjetas se cortan a mitad de palabra ("Fotocamer-a"). Arreglado en `fix/T14-T15`
      (4713299, 7650225) y capturas IT repetidas: válidas. Hay una 4.ª versión "general" del muro
      (ES/EN 6_4, IT 6_1): recomendada para la tienda. Anibal hace el resto de capturas en PRO y
      al final se eligen las de la tienda. Compilar y subir a TestFlight: más adelante.
- [x] `share_app_message` cambiado en EN/ES/IT (4713299, comprobado el 2026-11-11).
- [ ] Capturas ES revisadas (2026-11-11). Válidas: 2_3 (álbum Trabajo), 6_4 (muro general),
      3 (detalle con "Buscar similares", de reserva). Rehacer: 4 (fondo Android/MIUI, nombre y
      correo de Anibal, diálogo tapando la selección), 5 (saludos de terceros y DAT5 de
      protagonista: hacerla con placas). Falta la 1. ESCRIBIR_FOTO: ⚠️ contradice
      `decisiones/2026-11-02-anotar-y-compartir.md` (no anunciar T10 en capturas); decide Anibal.
- [ ] Selección ES (2026-11-11): 1 falta · 2_3 · 3 · 4_2 · 5_5 · 6_1 (general) · 7 ESCRIBIR_FOTO.
      EN e IT: mismas escenas con la app en ese idioma; en la 7, el texto escrito en EN/IT.
      EN revisadas (2026-11-11): 3_1+3_2 · 4_2 · 6_1 · 7 ESCRIBIR_FOTO_eng válidas. Rehacer: 5 (Wi-Fi
      encendido junto al avión) y 2 (álbum "Work" mezcla cajas y batidoras de tienda). Falta la 1.
- [ ] Próxima versión · T17–T21 (foto buscada primera, orden y orden en álbumes, compartir hacia
      iSIMILAR, avisos de "0 results" y 250/247): `borradores/2026-11-11-proxima-version-busqueda-album-compartir.md`.
- [ ] Capturas EN completas salvo la 1: 2_5 (álbum Work) · 3_1+3_2 · 4_2 · 5_1 · 6_1 · 7.
- [ ] Próxima versión · editor: zoom con dos dedos para señalar detalles (hoy los dos dedos
      cambian el tamaño del texto). Va con el arreglo de solapamientos.
- [ ] Próxima versión · muro ES: "Solo €1.08/mes" con formato inglés (debe ser "1,08 €/mes").
- [ ] Con la compilación en TestFlight / prueba interna: 7 días gratis con usuario nuevo y
      restaurar compras tras reinstalar. Después, enviar a revisión y liberar.

## Siguiente sesión (cierre del 2026-11-10)
1. **Leer el buzón de `solopila`**: hay una entrada nueva sin leer ("T15 y T16 hechos, T14
   pendiente de caducar", commit 9e14493 en `fix/T14-T15`).
2. Prueba de los 7 días gratis + caducidad (cierra también T14), en iPhone y Android.
3. Capturas: iPhone 13 para App Store (marco 1290 × 2796) y emulador Pixel para Google Play
   (marco 1080 × 1920). Ver `borradores/2026-10-24-capturas-tienda.md`, secciones finales.
4. hq: `tono-de-marca` para los textos de T10 y T13; después, el encargo de diseño de los marcos
   y los textos de la ficha.
5. Unir `fix/T14-T15` a `main` cuando T14, T15 y T16 estén probados → compilación final →
   7 días + restaurar compras sobre esa compilación → enviar a revisión.

## Nuevo 2026-11-02 · T10 escribir sobre una foto y compartir
- [x] `solopila` programa T10 (`borradores/2026-11-02-anotar-y-compartir.md`) y lo informa en el
      buzón (rama `feature/T10-anotar`, etiqueta `antes-de-T10`).
- [x] `solopila`: lápiz a la vista (fila propia "Escribir") y confirmar al cancelar (commits
      9603177 y 94dfbaf; cancelar probado por Anibal).
- [x] **T15 · Marca de agua en posición B (abajo a la izquierda)** (e4c504a, probado en iPhone y Mi A3 el 2026-11-10): elegida el 2026-11-09
      tras la prueba real en WhatsApp (iPhone y Mi A3). Falta que `solopila` la aplique en `fix/T14-T15`.
- [x] **T16 · Carpetas nuevas en Android entran marcadas** (33a89ac, 7/7 en Mi A3 el 2026-11-10) (opción A, en esta versión, en
      `fix/T14-T15`). Pruebas en `borradores/2026-11-06-antes-de-tiendas-t14-t15.md`.
- [x] T10+T13 unidos a `main` (commit 342c54f, 2026-11-09).
- [x] Unir `feature/T10-anotar` (T10 + T13) a `main`: OK de Anibal el 2026-11-06. Probado en
      iPhone y Mi A3 (buzón 2026-11-06 12:36). Gmail iOS arreglado (9b2f1e4).
- [ ] **Próxima versión · solapamientos del editor al escribir:** "✓" tapa "Compartir"; los
      colores tapan "Texto" y "Deshacer". Arreglo previsto: ocultar "Compartir" y la fila de
      herramientas mientras se escribe (`annotate_editor.dart`). No usar el editor en las capturas
      de la tienda hasta arreglarlo.
- [x] **T14 · Estado PRO único** (commit b23505d; caducidad probada en iPhone y Mi A3 el 2026-11-10): comprar y PRO en modo avión, probados. Falta
      probar que una suscripción de prueba caducada pasa a gratis (iPhone y Mi A3).
- [x] Acceso completo a las fotos al arrancar: se mantiene y no se revisa (Anibal, 2026-11-06;
      `decisiones/2026-11-06-antes-de-tiendas.md`).
- [ ] **T12 · Copias de fotos en la caché** (2026-11-02): en el iPhone hay 10 carpetas con fotos
      en la caché, anteriores a T10. T10 deja `tmp` limpio. Sospechosos sin confirmar: copias
      de `photo_manager` al pedir `asset.file` (visor: tamaño de la foto; compartir en lote),
      con `PhotoManager.clearFileCache()` comentado en `home_view_model.dart:311`, y fotos de la
      cámara de `image_picker` en Android (`TempFilesCleaner` solo limpia en iOS). Anibal quiere
      que se borren solas. Comprobar también que "Reset App" las borra (lo promete `/delete-data/`).
      Ojo: la limpieza nunca debe borrar la foto base de la cámara mientras se usa (ver T13).
- [x] **T13 · Foto de la cámara: "Ver", escribir y guardar** (commit b079491, probado en iPhone
      y Mi A3). La foto guardada aparece en las búsquedas tras "Escanear fotos nuevas".
      Para T12: no borrar `<cache>/base_image/`; sí incluir las copias de `share_plus`
      (`Library/Caches/<uuid>/` en iOS, `cache/share_plus` en Android), que hoy no borra ni
      `TempFilesCleaner` ni "Reset App".
- [x] hq pasa los textos de T13 por `tono-de-marca` (2026-11-10: aptos sin cambios).
- [x] Anibal: fotos enviadas por WhatsApp (vertical y horizontal): al abrir la foto, la marca
      se lee bien. En la vista previa del chat, no (ver arriba).
- [x] ~~T11 · `paywall_trigger` no llega a RevenueCat~~ Falsa alarma (2026-11-02): llega bien.
      Anibal lo vio en Customers → Attributes: `paywall_trigger = annotate_limit`, junto con
      `gallery_size` y `use_case`. RevenueCat guarda solo el último motivo de cada usuario.
- [x] Anibal: `paywall_trigger = annotate_watermark` confirmado en RevenueCat (Android, 2026-11-02).
- [ ] Hueco de medición de T10: RevenueCat dice quién paga por T10, pero no cuántos usuarios
      gratis anotan y comparten (`annotate_share` va a Firebase Analytics, que no está activo).
      Se decide junto con el consentimiento de Analytics en la UE; no se añade nada ahora.
- [x] hq pasa los textos de T10 por `tono-de-marca` (2026-11-10: aptos sin cambios).
- [x] Anibal prueba en el iPhone y el Mi A3 (lista de pruebas de T10 y T13, 2026-11-06).
- [ ] A los 30 días de publicar: revisión según `decisiones/2026-11-02-anotar-y-compartir.md`.
      No tocar `docs/` hasta entonces.

## Siguiente sesión (cierre del 2026-10-31)
- App lista (T1–T9). Quedan en `solopila`: prueba de los 7 días con usuario nuevo (iOS y
  Android), subir versión y compilar. **No enviar a revisión** hasta tener capturas y ficha.
  2026-11-09: en iOS se ve el botón "7 días gratis" (solo prueba que la tienda ofrece la
  prueba). Falta, con un usuario de sandbox nuevo y en Android con una cuenta de prueba:
  hoja de compra con "gratis 7 días y después el precio" → PRO al momento → RevenueCat lo
  marca como prueba → cancelar y seguir PRO hasta el final → al caducar, todo a gratis (T14)
  → con el mismo usuario, el botón ya no dice "7 días gratis".
- Anibal hace capturas con la versión nueva en EN, ES e IT y las deja en `archivo/`; hq las
  revisa (`borradores/2026-10-24-capturas-tienda.md`, "Decisiones de hq") y prepara el
  encargo de Claude Design. Después: textos de la ficha.
- Web, cuando se abra: buzón `PARA-HQ-DE-WEB.md`, añadir "compartir", tiempo de escaneo,
  y política + `/delete-data/` (publicar justo antes de liberar la versión).

## Para Anibal (tareas manuales, fuera del código)

### Documentos (`docs/`: los edita Claude con autorización de Anibal)
- [x] `definicion-tecnica.md` · Rendimiento medido: Xiaomi Mi A3, unas 8.000 fotos, 4-5 minutos
      (actualizado por Anibal el 2026-10-23, comprobado).
- [x] `definicion-tecnica.md` · Qué hace: funciones que la web ya menciona (añadidas el 2026-10-23):
      detalle de la foto (fecha, resolución en píxeles, peso); ordenar resultados por más o
      menos parecidas y por más o menos recientes; visor de álbumes creados desde la app (con
      detalle y búsqueda desde la foto).
- [ ] **Precio (se revisa al terminar la app):** brief y definición técnica dicen "12 € en la
      zona euro"; Anibal configuró 12,99 y cada tienda lo convierte con impuestos. Falta decidir
      qué precio se dice y dónde. La web hoy dice (EN): "Annual subscription with a 7-day free
      trial. You won't be charged if you cancel before the trial ends. The exact price for your
      country is shown in the store." + "Unlimited camera searches" + "Batch actions: delete,
      move or share many photos at once".
      Dato nuevo (sesión de la app, 2026-10-26): Google Play Italia cobra **15,99 €** y App Store
      Italia **12,99 €** (Play ya cobraba 15,99 en marzo). Revisar en Play Console el precio del
      plan base por país.
- [x] **⚠️ Contradicción · tiempo de escaneo** (sesión de la app, 2026-10-26). `docs/` corregido
      el 2026-10-30 (commits 88ed563 y 24a593b).
      Documento dice (`definicion-tecnica.md`, Rendimiento medido): "Primer escaneo, 15.000
      fotos, iPhone 13: entre 2,5 y 3 minutos".
      Medición dice: **15.700 fotos en 3:30** en iPhone 13 (iOS 26.6.2), modo profile
      (equivalente a producción), instalación desde cero. Ritmo ~75 fotos/s → **15.000 fotos
      en ~3:20**. Una medición anterior coincide (13.700 fotos en 3:26).
      Impacto: cualquier texto con "2,5-3 minutos" (web, ficha, marketing) promete un 10-30 %
      más de velocidad de la real.
      Opciones: A) acelerar el escaneo (proyecto aparte, no esta versión); B) Anibal revisa el
      documento (p. ej. "unos 3-3,5 minutos para 15.000 fotos") y los textos que lo citen.
      **Decidido B (Anibal, 2026-10-30):** "unos 3 minutos y medio".
- [x] **`definicion-tecnica.md` · Datos y privacidad: FCM solo en Android** (sesión de la app,
      2026-10-26). La app de iOS no tiene la capacidad Push Notifications, así que en iOS nunca
      ha existido token de FCM (las notificaciones remotas nunca han funcionado en iOS). Desde
      T2 el token se crea solo en Android al activar el recordatorio. El recordatorio semanal es
      local y funciona en las dos plataformas. Push en iOS queda para el futuro (decisión de
      Anibal). Revisar la tabla de servicios y la etiqueta de la App Store con este dato.
      **Hecho (2026-10-30, commit 88ed563):** "solo Android" y que iOS lo tendrá en el futuro.

### Web
- [ ] Añadir "compartir" donde la web dice "mueve o borra en lote" (compartir en lote es PRO
      desde el 2026-10-23). Buscar "move or delete", "mueve o borra", "sposta o elimina",
      "in bulk", "en lote", "in blocco" en `astro/src/i18n/*.json` (al menos `description` y
      `ogDescription` de "cómo funciona"). Mismo orden en los 3 idiomas: mueve, borra o comparte.
- [ ] Tiempo del primer escaneo: "unos 3 minutos y medio" en EN/ES/IT
      (`borradores/2026-10-30-web-tiempo-escaneo.md`), en una sesión de la web.
- [x] Subida de `astro/dist/` a isimilar.app (confirmado por Anibal el 2026-10-24).
      Comprobado: `/en/` redirige a la portada (301), `i18n.js` ya no existe (404) y el
      sitemap responde (200).
- [ ] Dar de alta la web y el sitemap (`https://isimilar.app/sitemap-index.xml`) en Google
      Search Console y en Bing Webmaster Tools (Bing alimenta a ChatGPT y Copilot).

### Tiendas y paneles
- [ ] **App Store Connect:** etiqueta de privacidad: identificadores y compras como
      vinculados, sin rastreo; quitar "Datos de rendimiento". No requiere versión nueva.
      Comprobar también que no declara el token de notificaciones (FCM): en iOS no existe
      (añadido el 2026-10-30). RevenueCat envía por su cuenta el estado de ATT ("Not
      determined": la app nunca pide rastrear); no cambia la respuesta "sin rastreo".
- [ ] **Google Play Console:** formulario de seguridad de datos coherente con la etiqueta,
      incluidos Cloud Messaging y Remote Config. "Contiene anuncios: No".
- [ ] **Ambas tiendas:** URL de privacidad `https://isimilar.app/privacy/`; en Google Play,
      URL de borrado de datos `https://isimilar.app/delete-data/`.
- [ ] **App Store Connect:** descripción de la ficha con los cambios de
      `borradores/2026-10-22-ficha-y-muro.md` (en el próximo envío).
- [x] **Panel de RevenueCat:** sin integraciones con terceros; el borrado se pide con el ID
      de usuario de RevenueCat (comprobado el 2026-10-22, recogido en `definicion-tecnica.md`).

## Esperando decisión de Anibal (2026-10-26)
- ~~Capturas: contradicciones 1 y 2~~ Resueltas el 2026-10-31 (sección "Decisiones de hq" de
  `borradores/2026-10-24-capturas-tienda.md`). 2026-11-09: Anibal empieza las capturas en
  paralelo a T14–T16, sin el editor de T10 en ninguna captura.
- Vídeo de búsquedas: A (cortar) o B (desenfocar) y destino (ficha o redes).
- Precio de Google Play Italia 15,99 € vs App Store 12,99 €: corregir en Play Console.
- Muro de pago: alcance del rediseño (recomendado: solo textos y cabecera por acción en esta
  versión; rediseño visual después, valorando el editor de muros de RevenueCat).
- Redes: idioma del contenido de YouTube/Facebook; ¿Instagram?; ¿qué hacer con la cuenta de
  TikTok?

## App (sesión en `solopila/`)
Instrucciones completas y en orden: `borradores/2026-10-22-instrucciones-app.md`.
- [x] T1: quitar `firebase_analytics` (commit 9b2375e de `solopila`).
- [x] T2: retrasar el token de notificaciones (commits 24fcdfa y a69309c).
- [x] T3: Firebase Performance Monitoring no se usa (resultado en `solopila/HISTORY.md`,
      commit 2eaae3d).
- [x] T4 (commit 2eaae3d): precio de respaldo $12.99 (solo el precio de la tienda). Botón siempre activo y
      mensaje traducido en errores de red (`decisiones/2026-10-30-boton-pago-sin-precio.md`).
- [x] T4i (commit d6304eb): Restaurar compras sin compras → aviso y el muro queda abierto.
- [ ] Antes de enviar a tiendas: probar reinstalar la app → "Restaurar compras" → vuelve a
      ser PRO. Comprobar también si "Reset App" hace perder el reconocimiento de la compra.
- [x] T4h (commit 340dfdf): entradas al muro en la pantalla principal (contador y botón "PRO"), después de T4i
      (`decisiones/2026-10-30-entradas-al-muro.md`).
- [x] T4b (commit 59d2ae7): interruptor "Compartir datos técnicos" en Ajustes. Al desactivarlo también borra
      los atributos ya enviados a RevenueCat (opción B, 2026-10-31).
- [ ] **Política de privacidad (EN/ES/IT) y formulario de Google Play por T4b:** mencionar el
      interruptor como forma de oponerse (apartados 5.2 y 5.3); en Google Play, informes de
      errores y datos de uso como opcionales. Borrador:
      `borradores/2026-10-31-privacidad-interruptor-t4b.md`. **Publicar a la vez que la
      versión de la app, no antes.** Decidido (2026-10-31): aplicar también B.4 (orígenes
      del muro, más `batch_share` si T4c sale en esta versión); la fecha compartida con los
      Términos se acepta; el formulario de Google Play se cambia con la versión al 100 %.
- [ ] **Día de publicación:** App Store con publicación manual y Google Play con publicación
      gestionada; subir la web (política y `/delete-data/`) justo antes de liberar.
      T4d (enlaces legales a la web) debe ir en esta misma versión.
- [x] T4c (commit 4923dcb): compartir en lote es PRO (hoy es gratis en `album_detail_sheet.dart:72-87`);
      `paywall_trigger` = `batch_share`.
- [x] T4f (commit 4923dcb): compartir en lote desde los resultados de búsqueda (hoy no existe), PRO, con
      `batch_share`. Va con T4c.
- [x] T4j (commit fa94b6c, probado en Mi A3): visor de álbumes, 1 foto gratis (como en todas partes) y panel de ayuda también en
      Android.
- [x] T4d (commit f27c4e7): enlaces legales de Notion → web, en el idioma de la app.
- [x] T4g (commit e6895e0): en Ajustes, cambiar TikTok (`@lifesolutionsapp`) por YouTube
      (`@iSIMILAR-APP`) y Facebook (`facebook.com/iSIMILAR`).
- [x] T4e: "Reset App" coincide con `/delete-data/` (informe de `solopila`, 2026-10-31). La
      página se completa con dos matices (sección H del borrador de privacidad T4b).
- [x] T5–T8: textos del muro de pago (Anibal, 2026-10-31; en pruebas).
- [x] T9 (commit 8ae6218): textos del muro y del acordeón de inicio más claros y vendedores, dentro del brief
      (`borradores/2026-10-31-textos-muro-y-acordeon-t9.md`).
- [x] Diálogo previo al muro (commit 4923dcb): Anibal elige A (abrir el muro directamente con cabecera según la
      acción), 2026-10-26. Decisión en `solopila/docs/decisiones/2026-10-26-dialogo-previo-al-muro.md`.
      Va con T4c/T4f. Rediseño del muro: ver respuesta del 2026-10-26 (alcance a decidir).
- [ ] Al terminar: volver a hq y decir "app lista".

## Web (hecho el 2026-10-23)
- [x] Copia del servidor en `solopila_landingPAGE/servidor-2026-10-22/` (commit 3227d52).
- [x] Web en Astro (`solopila_landingPAGE/astro/`) publicada en isimilar.app, EN/ES/IT.
- [x] Legales v3 publicados (`/privacy/`, `/terms/`, `/delete-data/`), con datos del
      responsable en `astro/src/legal/datos.json` (sin REA; correo info@isimilar.app).
- [x] Términos v3.1 (legal-tiendas): planes actualizados y precio sin importe fijo
      (`borradores/2026-10-23-legal-terminos-v3.1.md`). Subido el 2026-10-24.
- [x] Correcciones de Anibal (`borradores/2026-10-23-web-correcciones-anibal.md`) y ajustes
      de growth (`borradores/2026-10-23-web-ajustes-growth.md`). Subido el 2026-10-24.
- [x] Brief y definición técnica: compartir en lote es PRO; de una en una, gratis.

## Decisiones de Anibal (2026-10-23)
- Definición: "buscador privado de imágenes similares para la galería del teléfono".
- FAQ de duplicados: "placas electrónicas de distintas reparaciones" (no "la misma placa").
- Compartir en lote: se publica en la web aunque la versión de la app salga después.
- Una sola acción (borrar, mover, compartir) siempre es gratis. Todas las acciones en lote, PRO.
- Sin precio fijo en la web: "Suscripción anual con 7 días de prueba gratis. El precio exacto
  de tu país se muestra en la tienda."
- Sin anuncios: "La app se financia con las compras de PRO, no con publicidad."
- Sin pago único: PRO es siempre una suscripción anual. Unificado en brief y guía el
  2026-10-24 (`decisiones/2026-10-24-sin-pago-unico-y-regla-docs.md`).
- Sin revisión de abogado por ahora (sin presupuesto).
- Fecha del detalle de la foto: escribir solo "la fecha" (no se sabe si es de captura o de
  guardado).

### Dudas de growth respondidas (2026-10-23)
1. "Pantallas de móvil" = fotos de pantallas físicas de celulares. No mencionar en público
   que se fotografían emails o contraseñas de clientes (RGPD y tono).
2. Compartir en lote: PRO.
3. La app funciona en modo avión desde la primera apertura.
4. El pie enlaza a páginas de la web, no a Notion.
5. Se mantiene la FAQ "¿Es un limpiador de duplicados?", con nombres verificados de las
   herramientas y sin decir nada negativo de ellas.

## App · próxima versión técnica (después de esta)
- [ ] Actualizar los paquetes de Firebase (core 4.5→4.15, crashlytics 5.0.8→5.4, messaging
      16.1.2→16.7, remote_config 6.2→6.7) en una tarea propia, con prueba en dispositivo de
      notificaciones, Crashlytics, Remote Config y compras. Decidido el 2026-10-24: esta
      versión sale con el `pubspec.lock` de producción (opción A).
- [ ] Subir `IPHONEOS_DEPLOYMENT_TARGET` a 15.0 (límite primavera 2027). Recomendado en esta
      versión (el Podfile ya está en 15.0); si no entra, va con la de Firebase.

## A decidir con datos (después de publicar esta versión)
- [ ] **Límite en lote durante la prueba** (propuesta de Anibal, 2026-10-24): hasta 30 fotos
      por acción durante los 7 días de prueba, sin límite al pagar. No entra en esta versión.
      - Por qué: 5 de 6 pruebas canceladas y ninguna convertida; los 4 pagos llegaron sin
        prueba. Hipótesis sin comprobar: la prueba regala la limpieza grande.
      - Datos a mirar en RevenueCat: `batch_size` y `paywall_trigger` de quien empieza la
        prueba; si los que no tenían prueba la rechazaron o no tenían derecho a ella.
      - Antes de aplicar: avisos claros (muro y foto 31), y actualizar web, términos, ficha
        y `docs/`. Se decide junto con el precio.
      - 30 es una intuición, no un dato. Alternativa si no funciona: quitar la prueba.

## Ideas de producto (más adelante, sin decidir)
- [ ] **Idea "Encuentra lo que no buscabas"** (2026-10-24): segundo ángulo emocional,
      lluvia de ideas y riesgos en `borradores/2026-10-24-idea-recuerdos.md`.
- [ ] **Texto encima de las fotos** (2026-10-25): escribir un texto sobre una foto encontrada,
      estilo TikTok o meme, y compartirla (caso real de Anibal: foto de 2018 para un familiar).
      Se guarda como foto nueva; el original no se toca. Pendiente decidir gratis o PRO,
      alcance (solo texto o también tipografías y colores) y si lleva marca de iSIMILAR.
- [ ] **"Compartido desde iSIMILAR"** (2026-10-25): marca al compartir. Opciones a decidir:
      texto en el mensaje (no en la foto), marca solo en las fotos con texto, o marca en
      todas. Ver la revisión del 2026-10-25.

- [ ] **Notificaciones de novedades** (2026-10-26): Anibal quiere usar push de Firebase en el
      futuro. Hacerlo con un interruptor propio en Ajustes ("Recibir novedades de iSIMILAR")
      que cree el token solo a quien lo active, más una línea en la política y revisión de
      las etiquetas de las tiendas. Contexto: con T2 (opción A) el token solo existe si el
      recordatorio semanal está activo; nunca se ha enviado una push desde la consola.

- [ ] **Serie de tutoriales en YouTube** (2026-10-26): cómo se usa la app y contacto con
      usuarios en los comentarios. Pendiente: idioma(s), lista de capítulos, y encaje con el
      plan de vídeos de la guía (vídeos del fundador en su taller).

## Más adelante
- [ ] Ficha de App Store para México.
- [ ] Pantalla de consentimiento (cuando se reactive Analytics).
- [ ] Revisión de la política y los términos por un abogado (cuando haya presupuesto).
- [ ] Estrategia de contenido de autoridad (fotos en el móvil y privacidad).
- [ ] Web, Fase 4: páginas de casos de uso por segmento.
- [ ] Imagen de vista previa (`og:image`) por idioma, sin "100% OFFLINE PRIVACY".
