# iSIMILAR — Centro de mando (negocio)

Carpeta para marketing, contenido, legal, monetización y estrategia de iSIMILAR.
Mantener este archivo por debajo de 80 líneas: aquí solo va el índice y las reglas.
Lo nuevo se guarda en `docs/`, nunca aquí.

## Qué es iSIMILAR (una línea)
Buscador visual privado para la galería del móvil: eliges una foto o apuntas la
cámara y encuentra las parecidas, todo dentro del teléfono. Gratis buscar; PRO
anual (12 € / 11,99 USD, 7 días de prueba) para acciones en lote.

## Carpetas
- `../solopila/` → código de la app Flutter. **Solo lectura desde aquí.**
  Para programar, abrir Claude Code directamente en esa carpeta.
- `../solopila_landingPAGE/` → web isimilar.app. **La versión publicada es `Nueva/`.**
  Para editarla, abrir Claude Code en esa carpeta.
- `docs/` → documentos vigentes · `docs/decisiones/` → decisiones con fecha
- `docs/archivo/` → versiones antiguas (no usar como fuente)
- `borradores/` → textos, guiones y propuestas en elaboración

## Fuentes de verdad (en este orden)
- **Técnico:** el código de `../solopila` y su `CLAUDE.md`. Después
  `docs/definicion-tecnica.md`. Si el documento contradice al código, manda el
  código: avisar y proponer la corrección del documento.
- **Comercial:** `docs/brief-marketing.md` (qué se dice y cómo) y
  `docs/guia-estrategica.md` (mercado, clientes, plan de 8 semanas).
- **Anuncios de pago:** `docs/estrategia-anuncios.md` (decisión pendiente).
- Leer el documento relevante ANTES de responder sobre iSIMILAR.

## Cómo colaborar conmigo (Anibal)
- Cuestiona todo: pros, contras y riesgos reales. Destruye los argumentos débiles
  con lógica, vengan de quien vengan. Nada de seguirme la corriente.
- Dime lo que necesito, no lo que quiero oír. Preciso, sin ilusiones ni pesimismo.
- Haz preguntas serias y verificables para llegar al mejor plan, y propón soluciones.
- Para revisar a fondo un plan o una idea, usar la skill `revisor-critico`.

## Agentes (`.claude/agents/`)
| Agente | Para qué |
|---|---|
| `growth` | Estrategia, posicionamiento, ASO, textos de tienda y web, visibilidad en IA |
| `contenido` | Investigación, guiones de vídeo, posts, ganchos, Reddit |
| `legal-tiendas` | Privacidad, RGPD, normas App Store / Google Play, suscripciones |
| `monetizacion` | Muro de pago, precio, prueba gratuita, datos RevenueCat y Analytics |

## Skills (`.claude/skills/`)
- `tono-de-marca` → revisar cualquier texto público antes de darlo por bueno
- `checklist-release` → antes de publicar una versión de la app o de la web
- `revisor-critico` → abogado del diablo para planes, ideas y decisiones

## Reglas fijas
- Nunca escribir "anónimos" para los datos: son seudónimos (RGPD).
- El precio y lo que incluye PRO debe ser idéntico en app, tienda, web y anuncios.
- Nada de "el primero", "0,5 s", "50 ms" ni "encuentra todas tus facturas".
- Decisión importante → nuevo archivo en `docs/decisiones/AAAA-MM-DD-tema.md`.
- Al cambiar un documento vigente, actualizar su fecha en la cabecera.
- No modificar archivos de `../solopila` ni de la web desde aquí sin orden explícita.

## Proyecto técnico activo
Destilación DINOv2 → MobileNetV3 (vector 960 → 384, obliga a re-escanear).
Plan completo en `../solopila/tools/distill/ROADMAP.md` (mientras no se aplique la
propuesta, sección 17 de `../solopila/CLAUDE.md`). No anunciar nada hasta medirlo.
