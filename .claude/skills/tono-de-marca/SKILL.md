---
name: tono-de-marca
description: Revisa cualquier texto público de iSIMILAR (web, ficha de tienda, capturas, anuncios, vídeos, posts, emails) contra el brief de marketing. Úsala antes de dar por bueno cualquier texto que vaya a ver un usuario.
---

# Revisión de tono y mensaje

1. Lee `docs/brief-marketing.md`, secciones "Posicionamiento, mensaje y tono",
   "Lo que se puede y no se puede decir" y "Precio y cómo comunicarlo".
2. Revisa el texto frase por frase y devuelve una tabla:
   frase original · problema · regla del brief que incumple · versión corregida.
3. Comprueba siempre:
   - Se apoya en un pilar: **Encuentra**, **Ordena** o **Privado**.
   - Ninguna promesa no verificable: "el primero", "exacta", "todas tus facturas",
     "0,5 s", "50 ms", "100% gratis", "anónimo", "tiempo ahorrado", "GB liberados".
   - Precio y PRO idénticos al brief (12 € / 11,99 USD anual, 7 días de prueba;
     lote siempre PRO). Nunca "5 free actions".
   - Tono directo, práctico, honesto. Sin "magia" ni superlativos.
   - Idioma natural del mercado (EN/ES/IT), con las palabras que busca la gente.
4. Si el texto describe una función, contrástala con `docs/definicion-tecnica.md`.
   Si el texto contradice cualquiera de los 3 documentos, márcalo como
   "⚠️ Contradicción detectada" (formato de CLAUDE.md); no corrijas el documento.
5. Termina con un veredicto: **apto**, **apto con cambios** o **no apto**.
