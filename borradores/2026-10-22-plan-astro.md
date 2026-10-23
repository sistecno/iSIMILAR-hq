# Plan de migración de isimilar.app a Astro (para la sesión en `solopila_landingPAGE/`)

Estado: propuesta. Decisiones de base en `decisiones/2026-10-21-web-astro-seo.md`.
Textos: `borradores/2026-10-21-web-fase1-textos.md` (growth). Legal: pendiente de
`borradores/2026-10-22-legal-politicas-v2.md`.

## Requisitos previos (Anibal)
1. **Copia del servidor (Fase 0):** con FileZilla, descargar la carpeta completa de
   isimilar.app, incluidos los ocultos (`.htaccess`; en FileZilla: Servidor → Forzar mostrar
   archivos ocultos), a `solopila_landingPAGE/servidor-2026-10-22/`. Commit.
2. Responder las dudas 1, 2, 3, 6 y 8 del borrador de growth (sección 10).
3. Abrir Claude Code en la carpeta de la web:
   `cd ~/Documents/Flutter/solopila_landingPAGE && claude`

## Estructura en el repo
```
solopila_landingPAGE/
├─ web/                  ← web actual, intacta hasta que la nueva esté publicada
├─ servidor-2026-10-22/  ← copia del servidor (Fase 0)
├─ astro.config.mjs
├─ package.json          ← Astro + @astrojs/sitemap (versiones exactas)
├─ public/               ← .htaccess, robots.txt, favicons, og-image
├─ src/
│  ├─ i18n/              ← en.json, es.json, it.json (textos de cada página)
│  ├─ components/        ← Nav, Footer, LangSwitch, StoreButtons, Pricing (precio en un solo sitio)
│  ├─ layouts/Base.astro ← <head>: title, description, canonical, hreflang, og, JSON-LD
│  ├─ assets/            ← imágenes sacadas del base64 de index.html, optimizadas por Astro
│  └─ pages/
│     ├─ index.astro, how-it-works.astro, faq.astro
│     ├─ es/index.astro, es/como-funciona.astro, es/preguntas-frecuentes.astro
│     └─ it/index.astro, it/come-funziona.astro, it/domande-frequenti.astro
└─ dist/                 ← lo que se sube con FileZilla (en .gitignore, igual que node_modules/)
```

## Configuración técnica
- Astro estático, `output: 'static'`, `site: 'https://isimilar.app'`, `trailingSlash: 'always'`,
  `build.format: 'directory'`.
- `i18n`: `defaultLocale: 'en'`, `locales: ['en','es','it']`, `prefixDefaultLocale: false`.
- `@astrojs/sitemap` con i18n (genera alternates hreflang).
- `<head>` por página: `<html lang>` correcto, canonical propio, hreflang en/es/it + x-default,
  og:locale (`en_US`, `es_LA` + alternate `es_ES`, `it_IT`), `SoftwareApplication` (11.99 USD)
  en portadas, `FAQPage` en FAQ.
- Detección de idioma: script en línea solo en `/`; primera visita sin idioma guardado;
  `navigator.languages` es → `/es/`, it → `/it/`; el selector guarda la elección en
  localStorage (con try/catch). Nunca redirigir desde `/es/` ni `/it/`.
- `public/.htaccess`: 301 de `/en` y `/en/*` a `/`; redirección a https; 404 propia;
  caché larga para `/_astro/*`. Fusionar con el `.htaccess` que haya en el servidor (Fase 0).
- `robots.txt` con la URL del sitemap.
- Enlace de App Store neutro: `https://apps.apple.com/app/id6738889078`.
- Mismo diseño visual que la web actual (colores, Inter, componentes); sin analítica ni cookies.
  Externos permitidos: Google Fonts (o Inter autoalojada, preferible) y nada más.
- Pie: privacidad y términos apuntan temporalmente a Notion hasta tener `/privacy` y `/terms`.

## Orden de trabajo (commits pequeños, uno por paso)
1. Montar Astro (sin tocar `web/`), `npm run dev` funcionando. Actualizar `CLAUDE.md` de la web.
2. Layout, Nav, Footer y LangSwitch con el diseño actual.
3. Portada EN con los textos de growth; luego ES e IT.
4. Cómo funciona y FAQ en los 3 idiomas.
5. SEO técnico: hreflang, canonical, sitemap, robots, JSON-LD, `.htaccess`, detección de idioma.
6. Revisión: `tono-de-marca` sobre el resultado, Lighthouse, validar hreflang y JSON-LD,
   probar en móvil. `checklist-release` de hq.
7. Publicación (ver abajo).
8. Después: `/privacy`, `/terms` y borrado de datos cuando legal-tiendas y Anibal los cierren.

## Publicación con FileZilla
1. `npm run build` → revisar con `npm run preview`.
2. Commit con la etiqueta de versión.
3. Subir **el contenido** de `dist/` a la carpeta de isimilar.app (no la carpeta `dist/` en sí).
   Sobrescribir; no borrar nada del servidor en la primera subida.
4. Comprobar en el navegador: `/`, `/es/`, `/it/`, `/en/` (debe redirigir), `/sitemap-index.xml`,
   `/robots.txt`, idioma automático en una ventana privada.
5. Dar de alta el sitemap en Google Search Console y Bing Webmaster Tools.

**Deshacer:** subir de nuevo `servidor-2026-10-22/` con FileZilla (menos de 5 minutos).
