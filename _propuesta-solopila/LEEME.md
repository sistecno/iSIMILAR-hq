# Propuesta: reorganizar solopila/CLAUDE.md (832 → 82 líneas)

Nada de esto está aplicado aún. Los archivos de esta carpeta reproducen la ruta
que tendrían dentro de `solopila/`.

## Verificación
De las 635 líneas con contenido del CLAUDE.md original, todas están en estos archivos
salvo 6, a propósito: las 5 de la cabecera antigua (título, notas, "## 0.") y la regla
"Registrarla en este archivo (CLAUDE.md)", cambiada por "registrarla en docs/decisiones/".

## Cómo se aplicaría (con tu orden, en una rama git `reorg-claude-md`)
1. Copiar esta carpeta sobre `solopila/` (sustituye CLAUDE.md; crea docs/arquitectura,
   docs/decisiones, docs/archivo, docs/BACKLOG.md, tools/CLAUDE.md, tools/distill/ROADMAP.md).
2. Mover `docs/iSIMILAR_BRIEFING.md` → ya copiado a `iSIMILAR-hq/docs/archivo/`; quitar de solopila.
3. Mover `docs/ADVERTISING_STRATEGY.md` → ya copiado a `iSIMILAR-hq/docs/estrategia-anuncios.md`; quitar de solopila.
4. Mover `BUGS.txt` (2024, código ya eliminado) → `docs/archivo/BUGS-2024.txt`.
5. Commit; revisas el diff; si te convence, merge a tu rama principal.

Ningún archivo de código (`lib/`, `android/`, `ios/`, `tools/*.py`) se toca.
