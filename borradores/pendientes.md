# Pendientes de iSIMILAR

Actualizado: 2026-10-24. Marca con [x] lo hecho.

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

### Web
- [x] Subida de `astro/dist/` a isimilar.app (confirmado por Anibal el 2026-10-24).
      Comprobado: `/en/` redirige a la portada (301), `i18n.js` ya no existe (404) y el
      sitemap responde (200).
- [ ] Dar de alta la web y el sitemap (`https://isimilar.app/sitemap-index.xml`) en Google
      Search Console y en Bing Webmaster Tools (Bing alimenta a ChatGPT y Copilot).

### Tiendas y paneles
- [ ] **App Store Connect:** etiqueta de privacidad: identificadores y compras como
      vinculados, sin rastreo; quitar "Datos de rendimiento". No requiere versión nueva.
- [ ] **Google Play Console:** formulario de seguridad de datos coherente con la etiqueta,
      incluidos Cloud Messaging y Remote Config. "Contiene anuncios: No".
- [ ] **Ambas tiendas:** URL de privacidad `https://isimilar.app/privacy/`; en Google Play,
      URL de borrado de datos `https://isimilar.app/delete-data/`.
- [ ] **App Store Connect:** descripción de la ficha con los cambios de
      `borradores/2026-10-22-ficha-y-muro.md` (en el próximo envío).
- [x] **Panel de RevenueCat:** sin integraciones con terceros; el borrado se pide con el ID
      de usuario de RevenueCat (comprobado el 2026-10-22, recogido en `definicion-tecnica.md`).

## App (sesión en `solopila/`)
Instrucciones completas y en orden: `borradores/2026-10-22-instrucciones-app.md`.
- [ ] T1–T3: quitar `firebase_analytics`, retrasar el token de notificaciones, confirmar que
      no se usa Firebase Performance Monitoring.
- [ ] T4: precio de respaldo $12.99 (solo el precio de la tienda).
- [ ] T4b: interruptor "Compartir datos técnicos" en Ajustes.
- [ ] T4c: compartir en lote es PRO (hoy es gratis en `album_detail_sheet.dart:72-87`);
      `paywall_trigger` = `batch_share`.
- [ ] T4d: enlaces legales de Notion → web, en el idioma de la app.
- [ ] T4e: comprobar que "Reset App" hace lo que dice `/delete-data/`.
- [ ] T5–T8: textos del muro de pago.
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
      notificaciones, Crashlytics, Remote Config y compras. Junto con subir
      `IPHONEOS_DEPLOYMENT_TARGET` a 15.0 (límite primavera 2027). Decidido el 2026-10-24:
      esta versión sale con el `pubspec.lock` de producción (opción A).

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

## Más adelante
- [ ] Ficha de App Store para México.
- [ ] Pantalla de consentimiento (cuando se reactive Analytics).
- [ ] Revisión de la política y los términos por un abogado (cuando haya presupuesto).
- [ ] Estrategia de contenido de autoridad (fotos en el móvil y privacidad).
- [ ] Web, Fase 4: páginas de casos de uso por segmento.
- [ ] Imagen de vista previa (`og:image`) por idioma, sin "100% OFFLINE PRIVACY".
