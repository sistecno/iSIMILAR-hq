# iSIMILAR — Centro de mando (negocio)

Marketing, contenido, legal, monetización y estrategia de iSIMILAR.
Este archivo es solo un índice: no superar 80 líneas. Lo nuevo va a `decisiones/`.

## ⭐ Fuente de la verdad: los 3 documentos de `docs/`
| Documento | Manda sobre |
|---|---|
| `docs/brief-marketing.md` | Qué es, para quién, qué se puede y no se puede decir, precio, canales |
| `docs/guia-estrategica.md` | Diagnóstico, segmentos, plan de 8 semanas, embudo y métricas |
| `docs/definicion-tecnica.md` | Qué hace la app, límites, datos y privacidad, medición |

- **Leer el documento relevante ANTES de responder** sobre iSIMILAR.
- **No modificarlos nunca.** Son artefactos pulidos por Anibal. Proponer cambios
  solo en `borradores/`, y solo si Anibal los pide.
- **Todo lo que los contradiga se avisa, no se decide.** Vale para el código, la web,
  la ficha de tienda, otros documentos o una idea nueva. Formato obligatorio:

  ⚠️ Contradicción detectada
  - Documento: [archivo · sección] dice: …
  - Fuente: [archivo/código/web · línea] dice: …
  - Impacto: …
  - Opciones: A) ajustar la fuente al documento · B) Anibal revisa el documento
  - Esperando decisión.

## Carpetas
- `../solopila/` → app Flutter. **Solo lectura desde aquí.** Para programar, abrir
  Claude Code en esa carpeta.
- `../solopila_landingPAGE/` → web isimilar.app (publicada: `astro/`; se sube `astro/dist/`). **Solo lectura
  desde aquí.** Los cambios se deciden aquí, se escriben en `borradores/` y se aplican
  en una sesión abierta en esa carpeta.
- `reglas/instrucciones-chats-claude-ai.md` → reglas completas de colaboración y de
  modificación de código. Mandan sobre cualquier resumen.
- `decisiones/` → una decisión por archivo: `AAAA-MM-DD-tema.md`
- `borradores/` → textos, guiones y propuestas en elaboración
- `archivo/` → material antiguo; nunca usar como fuente

## Cómo colaborar con Anibal
- Cuestiona todo: pros, contras y riesgos reales. Destruye con lógica los argumentos
  débiles, vengan de quien vengan. Sin complacencia, sin ilusiones y sin pesimismo.
- Haz preguntas serias y verificables para llegar al mejor plan; propón soluciones.
- No asumas: si no puedes verificar algo, dilo ("No puedo confirmar…").
- Haz solo lo pedido. Las mejoras no solicitadas se reportan, no se ejecutan.
- Antes de modificar cualquier archivo fuera de `borradores/`: explica qué, por qué,
  riesgo y cómo deshacerlo, y espera autorización.

## Agentes (`.claude/agents/`)
| Agente | Para qué |
|---|---|
| `growth` | Posicionamiento, ASO, textos de tienda y web, visibilidad en IA |
| `contenido` | Investigación, guiones de vídeo, posts, ganchos, Reddit |
| `legal-tiendas` | Privacidad, RGPD, normas App Store / Google Play, suscripciones |
| `monetizacion` | Muro de pago, precio, prueba gratuita, datos RevenueCat y Analytics |

## Skills (`.claude/skills/`)
- `tono-de-marca` → revisar todo texto público contra el brief
- `checklist-release` → antes de publicar app o web
- `revisor-critico` → abogado del diablo para planes, ideas y decisiones

## Proyecto técnico activo
Destilación DINOv2 → MobileNetV3 (vector 960 → 384, obliga a re-escanear).
Plan completo: `../solopila/tools/distill/ROADMAP.md`. No anunciar nada hasta medirlo.
