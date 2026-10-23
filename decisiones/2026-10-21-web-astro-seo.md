# 2026-10-21 · Web isimilar.app: Astro, idiomas y SEO

Decidido por Anibal.

## Decisiones
- **Herramienta:** Astro en modo estático. Node solo en el Mac de Anibal
  (`npm run build` → `dist/`). Banahosting (plan multidominio) sirve solo HTML;
  se publica subiendo `dist/` con FileZilla a la carpeta de isimilar.app.
  Sin WordPress ni editor visual: solo edita Anibal.
- **Idiomas:** raíz `/` en inglés; `/es/` y `/it/`. `/en/` redirige (301) a `/`
  vía `.htaccess`. Se aparta de la guía (`guia-estrategica.md`, línea 43, pide `/en`);
  aceptado por Anibal.
- **Detección de idioma:** solo en `/`, en la primera visita y sin idioma guardado:
  navegador en español → `/es/`, en italiano → `/it/`, otro → inglés. Por JavaScript,
  nunca en el servidor y nunca desde `/es/` o `/it/`. La elección del selector se
  guarda y manda.
- **Contradicciones web vs brief:** opción A, la web se ajusta al brief
  (precio 11,99 USD, sin "el primero", "facturas", "gratis para siempre" a secas,
  "15 GB", "cero datos", "magia" ni comparativa Wi‑Fi/servidores).
- **Privacidad y términos:** hoy en Notion. Objetivo: `/privacy` y `/terms` en el
  dominio, revisados por `legal-tiendas`. No retirar las URL de Notion hasta
  actualizar los enlaces de la ficha y de la app.

## Fases
0. Anibal descarga con FileZilla la carpeta de isimilar.app → al repo de la web (commit).
1. Textos en `borradores/`: `growth` (mapa de páginas, textos EN/ES/IT, metadatos)
   y `legal-tiendas` (privacidad y términos). Revisión con `tono-de-marca`.
2. Montaje de Astro en una sesión abierta en `solopila_landingPAGE/`.
3. `checklist-release`, subida con FileZilla, sitemap en Google Search Console y
   Bing Webmaster Tools.
4. Páginas de casos de uso por segmento.

## Para más adelante (sin definir)
Contenido de autoridad sobre fotos en el móvil y privacidad: problemas reales
(Reddit, foros) → artículos con solución. Búsquedas largas y concretas, no
"similar photos". Comparaciones con Google Fotos solo con datos comprobables
y fechados. Agentes: `contenido` (investigación) y `growth` (búsquedas).

## Deshacer
La web actual queda en git (`solopila_landingPAGE`, commit 2fb6f9e) y en la copia
de la Fase 0.
