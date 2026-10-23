# Pendientes de iSIMILAR

Actualizado: 2026-10-22. Marca con [x] lo hecho.

## Antes de publicar la próxima versión de la app
- [ ] **Desarrollador (sesión en `solopila/`):** quitar `firebase_analytics`, retrasar el token
      de notificaciones y confirmar que no se usa Firebase Performance Monitoring.
      Instrucciones: `borradores/2026-10-22-instrucciones-app.md` (T1–T3).
- [ ] **Desarrollador:** precio de respaldo $12.99 y textos del muro (T4–T8).
- [ ] **Anibal, App Store Connect:** etiqueta de privacidad: identificadores y compras como
      vinculados, sin rastreo; quitar "Datos de rendimiento". No requiere versión nueva.
- [ ] **Anibal, Google Play Console:** formulario de seguridad de datos coherente con la
      etiqueta, incluidos Cloud Messaging y Remote Config.
- [x] **legal-tiendas:** política de privacidad con cada servicio, su base legal y cómo
      oponerse (`borradores/2026-10-22-legal-politicas-v3.md`). No publicar hasta que la app
      cumpla T1 y T2.
- [x] Decidido: identificadores, compras, uso y diagnósticos se declaran como vinculados en
      App Store Connect, sin rastreo.
- [x] Decidido: interruptor en Ajustes para oponerse (tarea T4b de la app). La política usa la
      "frase alternativa" del apartado 1 de la v3 (línea 758).
- [ ] **Anibal, panel de RevenueCat:** comprobar que no hay integraciones con terceros y si se
      puede buscar un cliente por número de pedido.
- [x] `guia-estrategica.md:202` actualizada por Anibal.
- [ ] **Anibal:** rellenar a mano los datos del responsable en los textos legales.
- [ ] **Anibal, App Store Connect:** descripción de la ficha con los cambios de
      `borradores/2026-10-22-ficha-y-muro.md` (en el próximo envío).

## Web (Astro)
- [x] **Anibal:** copia del servidor con FileZilla (incluidos los archivos ocultos) en
      `solopila_landingPAGE/servidor-2026-10-22/` (commit 3227d52, 2026-10-23).
- [x] **Anibal:** responder las dudas de growth para la web (ver abajo).
- [ ] Abrir la sesión en `solopila_landingPAGE/` y seguir `borradores/2026-10-22-plan-astro.md`.
      **Objetivo de Anibal: Astro subido el 2026-10-23**, con `/privacy` y `/terms` incluidas.
- [x] **Anibal:** datos del responsable para la v3 legal (2026-10-23). En la web:
      `solopila_landingPAGE/astro/src/legal/datos.json`. Sin REA. Correo: info@isimilar.app.
- [ ] **Anibal:** subir con FileZilla el contenido de `solopila_landingPAGE/astro/dist/` y comprobar
      `/`, `/es/`, `/it/`, `/en/` (redirige), `/privacy/`, `/sitemap-index.xml`, `/robots.txt`.
- [ ] **Anibal:** dar de alta el sitemap en Google Search Console y Bing Webmaster Tools.
- [x] **Anibal, docs:** brief y definición técnica actualizados (2026-10-23): compartir en
      lote es PRO; borrar, mover o compartir de una en una es gratis.

- [x] **legal-tiendas:** términos v3.1 sin importe fijo y con planes actualizados
      (`borradores/2026-10-23-legal-terminos-v3.1.md`), aplicados en la web el 2026-10-23.
- [ ] **Anibal:** subir `astro/dist/` (correcciones de textos, precios y términos v3.1).
- [ ] **Anibal, docs:** añadir a `definicion-tecnica.md` las funciones que la web ya menciona:
      detalle de la foto (fecha, resolución, peso), ordenar resultados por parecido y por fecha,
      visor de álbumes creados desde la app (con detalle y búsqueda desde la foto).

### Decisiones de Anibal sobre los ajustes de growth (2026-10-23)
- FAQ de duplicados: se queda "placas de distintas reparaciones" (opción A).
- Compartir en lote: se publica hoy, aunque la versión de la app salga después.
- Una sola acción (borrar, mover, compartir) siempre es gratis.
- (2026-10-23) Sin pago único: PRO es siempre una suscripción anual. Sin revisión de abogado
  por ahora (sin presupuesto). Términos v3.1 publicados en la web (planes y precio sin importe).

### Dudas de growth para la web (respondidas por Anibal el 2026-10-23)
1. "Pantallas de móvil" = **fotos de pantallas físicas** de celulares (p. ej. fotos de
   pantallas de clientes con emails y contraseñas, para recordarlas o gestionarlas).
2. Compartir en lote **aún no existe**; va en la próxima versión de la app y será **PRO**
   (todas las acciones en lote son PRO). La web lo incluye ya.
3. La app **funciona en modo avión desde la primera apertura**.
4. El pie enlaza a **páginas de la web** (`/privacy`, `/terms`), no a Notion: la próxima
   versión de la app enlaza a la web. Texto: `2026-10-22-legal-politicas-v3.md` (fuente de
   la verdad legal); se publican ya aunque la app se actualiza en paralelo. Van en Astro.
5. FAQ "¿Es un limpiador de duplicados?": se mantiene con la propuesta de Anibal (ver
   sección 10 del borrador de growth), con dos condiciones: verificar en la web los nombres
   de las herramientas antes de publicar y no decir nada negativo de ellas.

## Más adelante
- [ ] Ficha de App Store para México.
- [ ] Pantalla de consentimiento (cuando se reactive Analytics).
- [ ] Revisión de la política por un abogado (cuando haya presupuesto).
- [ ] Estrategia de contenido de autoridad (fotos en el móvil y privacidad).
