# Pendientes de iSIMILAR

Actualizado: 2026-10-23. Marca con [x] lo hecho.

## Para Anibal (tareas manuales, fuera del código)

### Documentos (`docs/`, solo los edita Anibal)
- [x] `definicion-tecnica.md` · Rendimiento medido: Xiaomi Mi A3, unas 8.000 fotos, 4-5 minutos
      (actualizado por Anibal el 2026-10-23, comprobado).
- [x] `definicion-tecnica.md` · Qué hace: funciones que la web ya menciona (añadidas el 2026-10-23):
      detalle de la foto (fecha, resolución en píxeles, peso); ordenar resultados por más o
      menos parecidas y por más o menos recientes; visor de álbumes creados desde la app (con
      detalle y búsqueda desde la foto).
- [ ] Precio en los docs: brief y definición técnica dicen "12 € en la zona euro"; Anibal
      configuró 12,99 y cada tienda lo convierte con impuestos. Dejar en los docs el precio
      configurado real. (La web y los términos ya no muestran importes.)

### Web
- [ ] Subir con FileZilla **todo el contenido** de `solopila_landingPAGE/astro/dist/`
      (con archivos ocultos visibles: lleva `.htaccess`). Incluye: correcciones de textos,
      cuadros de precio, términos v3.1 y el arreglo de `/en/`.
- [ ] Después de subir: comprobar que `isimilar.app/en/` lleva a la portada.
- [ ] Borrar del servidor `i18n.js` (de la web anterior) y, si se quiere, los archivos de
      `_astro/` que ya no estén en `dist/_astro/`. No borrar `.well-known`.
- [ ] Dar de alta la web y el sitemap (`https://isimilar.app/sitemap-index.xml`) en Google
      Search Console y en Bing Webmaster Tools (Bing alimenta a ChatGPT y Copilot).
- [ ] Probar en un iPhone y un Android reales: botones de tienda y "Empezar la prueba",
      QR desde el ordenador, idioma automático en ventana privada, vista previa en WhatsApp.

### Tiendas y paneles
- [ ] **App Store Connect:** etiqueta de privacidad: identificadores y compras como
      vinculados, sin rastreo; quitar "Datos de rendimiento". No requiere versión nueva.
- [ ] **Google Play Console:** formulario de seguridad de datos coherente con la etiqueta,
      incluidos Cloud Messaging y Remote Config. "Contiene anuncios: No".
- [ ] **Ambas tiendas:** URL de privacidad `https://isimilar.app/privacy/`; en Google Play,
      URL de borrado de datos `https://isimilar.app/delete-data/`.
- [ ] **App Store Connect:** descripción de la ficha con los cambios de
      `borradores/2026-10-22-ficha-y-muro.md` (en el próximo envío).
- [ ] **Panel de RevenueCat:** comprobar que no hay integraciones con terceros y si se
      puede buscar un cliente por número de pedido.

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
      (`borradores/2026-10-23-legal-terminos-v3.1.md`). Pendiente de subir (ver arriba).
- [x] Correcciones de Anibal (`borradores/2026-10-23-web-correcciones-anibal.md`) y ajustes
      de growth (`borradores/2026-10-23-web-ajustes-growth.md`). Pendiente de subir.
- [x] Brief y definición técnica: compartir en lote es PRO; de una en una, gratis.

## Decisiones de Anibal (2026-10-23)
- Definición: "buscador privado de imágenes similares para la galería del teléfono".
- FAQ de duplicados: "placas electrónicas de distintas reparaciones" (no "la misma placa").
- Compartir en lote: se publica en la web aunque la versión de la app salga después.
- Una sola acción (borrar, mover, compartir) siempre es gratis. Todas las acciones en lote, PRO.
- Sin precio fijo en la web: "Suscripción anual con 7 días de prueba gratis. El precio exacto
  de tu país se muestra en la tienda."
- Sin anuncios: "La app se financia con las compras de PRO, no con publicidad."
- Sin pago único: PRO es siempre una suscripción anual.
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

## Más adelante
- [ ] Ficha de App Store para México.
- [ ] Pantalla de consentimiento (cuando se reactive Analytics).
- [ ] Revisión de la política y los términos por un abogado (cuando haya presupuesto).
- [ ] Estrategia de contenido de autoridad (fotos en el móvil y privacidad).
- [ ] Web, Fase 4: páginas de casos de uso por segmento.
- [ ] Imagen de vista previa (`og:image`) por idioma, sin "100% OFFLINE PRIVACY".
