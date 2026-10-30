# Web: tiempo del primer escaneo (2026-10-30)

**Estado:** listo para aplicar. `docs/` ya actualizado con autorización de Anibal (2026-10-30).

**Motivo:** medido en iPhone 13 (iOS 26.6.2, modo profile, instalación desde cero):
15.700 fotos en 3:30, unos 3:20 para 15.000. La web dice 2,5-3 minutos.
Decisión de Anibal (2026-10-30): decir "unos 3 minutos y medio".

**Dónde:** `solopila_landingPAGE/astro/src/i18n/{en,es,it}.json`, líneas 87 y 134 de cada
archivo. Solo cambia la frase del iPhone; lo del Xiaomi Mi A3 se queda igual.

| Idioma | Antes | Después |
|---|---|---|
| EN (87) | it takes 2.5 to 3 minutes; | it takes about 3.5 minutes; |
| EN (134) | On an iPhone 13 with 15,000 photos, 2.5 to 3 minutes. | On an iPhone 13 with 15,000 photos, about 3.5 minutes. |
| ES (87) | tarda entre 2,5 y 3 minutos; | tarda unos 3 minutos y medio; |
| ES (134) | En un iPhone 13 con 15.000 fotos, entre 2,5 y 3 minutos. | En un iPhone 13 con 15.000 fotos, unos 3 minutos y medio. |
| IT (87) | ci vogliono da 2,5 a 3 minuti; | ci vogliono circa 3 minuti e mezzo; |
| IT (134) | Su un iPhone 13 con 15.000 foto, da 2,5 a 3 minuti. | Su un iPhone 13 con 15.000 foto, circa 3 minuti e mezzo. |

**Después:** buscar "2.5", "2,5" y "3 min" en todo `astro/src` por si aparece en otro sitio
(datos estructurados, meta description), compilar y subir `astro/dist/`.
