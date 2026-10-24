# Idea: "iSIMILAR te encuentra los recuerdos" (2026-10-24)

Estado: idea en evaluación. No es una decisión. No cambia `docs/` hasta que Anibal lo decida.

## La observación (Anibal, tal cual)
Al empezar a buscar, encuentro imágenes que hace años que no veía y que ni recordaba que
tenía. Busco similares de una imagen, de los resultados elijo una y me trae otras nuevas; al
revisarlas veo fotos de hace un par de años que no recordaba y que haciendo scroll en la
galería nunca habría visto, porque yo nunca entro a la galería a ver fotos, y no conozco a
nadie que lo haga.

Conclusión de Anibal: "iSIMILAR te encuentra los recuerdos" (frase mejorable). Tenemos una
emoción de la app: no vender funcionalidades, vender emociones.

## Mecanismo real que lo produce
La búsqueda en cadena (`docs/definicion-tecnica.md`, Qué hace, punto 5): cada resultado abre
una búsqueda nueva, y los resultados no dependen de la fecha, así que salen fotos antiguas
mezcladas con las recientes.

## Frases candidatas (sin validar con `tono-de-marca`)
- "Busca una foto. Encuentra recuerdos."
- "Fotos que habías olvidado que tenías."
- "Una foto te lleva a otra. Y a recuerdos que habías olvidado."
- "Redescubre tu galería, foto a foto."

## Revisión crítica (resumen)
- A favor: ataca el mayor riesgo de la guía ("es un trabajo puntual": se limpia una vez y se
  olvida la app). Redescubrir da una razón para volver. Es una emoción real que vivió Anibal.
- En contra:
  1. Apple Fotos y Google Fotos ya venden esta emoción ("Recuerdos"), gratis y sin esfuerzo.
     Diferencia de iSIMILAR: lo guías tú desde cualquier foto, encadenando, y sin internet.
  2. No paga directamente: buscar es gratis; PRO son las acciones en lote. Sirve para
     descargas, retención y contenido, no para convertir.
  3. Público distinto: los 4 pagos llegaron por la App Store en inglés y decidieron en minutos
     (guía); no sabemos para qué usan la app. El brief apuesta por el uso profesional. Cambiar
     el posicionamiento principal sin datos sería apostar a ciegas.
  4. Matiz con la guía ("Encontrar una foto vieja choca con el producto"): la idea no es
     buscar una foto concreta, sino toparse con fotos olvidadas. Hay que decirlo así.
  5. Prueba de uno: le pasa a Anibal. No sabemos si les pasa a otros ni si lo valoran.
- Veredicto: ajustar. Probarlo como ángulo de contenido y, si funciona, como variante de
  capturas (prueba A/B de App Store), sin tocar el posicionamiento principal todavía.

## Preguntas abiertas
1. ¿Les pasa a otros usuarios? Preguntar a 5–10 conocidos que usen la app sin explicarles nada.
2. ¿Qué vídeo engancha más: "trabajo" o "recuerdos"? Mismo formato, misma cuenta.
3. ¿La gente vuelve a abrir la app por esto? Sin Analytics, solo se puede intuir.

## Aclaración de Anibal (2026-10-24)
- Apple y Google muestran recuerdos **elegidos por la app**; son un par de fotos que se ven y
  se dejan. iSIMILAR da otra emoción: **encontrar sin saber qué estás buscando**, guiado por ti.
- Es un segundo ángulo y un refuerzo del uso. Prioridad: descargas y uso habitual, aunque al
  principio no paguen. La monetización se resuelve después.

## Lluvia de ideas (sin filtrar, nada decidido)

### Frases
- ES: "Encuentra lo que no buscabas." · "Tira del hilo." · "Piérdete en tus propias fotos." ·
  "Tu galería tiene historias. Tira del hilo." · "Una foto te lleva a otra."
- EN: "Find what you weren't looking for." · "Pull the thread." · "Get lost in your own photos."
- IT: "Trova quello che non cercavi." · "Tira il filo." · "Perditi nelle tue foto."
- Juego con el concepto del brief ("Encuentra lo que buscas mirando, no escribiendo"):
  "Encuentra lo que buscas… y lo que no."

### Producto (ideas para más adelante; no se ejecutan)
1. Botón "Sorpréndeme": arranca una cadena desde una foto antigua al azar.
2. Marca de antigüedad en los resultados ("hace 3 años"), para que se note el hallazgo.
3. Rastro de la cadena (placa → perro → playa 2019), que se puede volver a recorrer.
4. "Guardar este hilo" como álbum: puente natural hacia PRO (mover en lote).
5. Recordatorio semanal (ya existe) reenfocado: "Tienes fotos de hace 2 años esperándote".
   Sin incluir fotos ni datos en la notificación.
6. Tarjeta para compartir: "Encontré esto de 2019 con iSIMILAR" (la foto la elige el usuario).
7. Widget de pantalla de inicio con una foto olvidada que abre una cadena.
8. Contador personal: "Has redescubierto 37 fotos de más de 2 años" (solo en el teléfono).

### Contenido
1. Serie "Tira del hilo": empezar en una foto cualquiera, 5 saltos, revelar la más antigua.
2. Reacciones: dar la app a alguien (madre, amigo) y grabar qué encuentra.
3. Mascotas: una foto del perro → todos los años de su vida. (Las capturas antiguas ya usaban
   un perro con 69 resultados.)
4. Fechas señaladas: una foto de la Navidad pasada → todas las Navidades.
5. Contraste: "Apple elige qué recuerdas. Aquí eliges tú."
6. Reto para usuarios: publicar su hilo más largo o su hallazgo más antiguo.

### Tienda
- Variante de capturas para la prueba A/B: "Find what you weren't looking for".
- Palabras clave a estudiar con `growth`: rediscover, old photos, forgotten photos.

## Riesgos que siguen abiertos
- Sin Firebase Analytics no se mide el uso habitual. Fuentes posibles: retención de App Store
  Connect (solo usuarios que aceptan compartir datos) y renovaciones. Si la estrategia es
  "descargas y uso", la medición pasa a ser prioritaria (consentimiento en la UE).
- Contenido con fotos personales: solo propias o con permiso; nada de caras de terceros ni
  menores sin consentimiento.
- Todo texto público debe pasar `tono-de-marca` y no prometer "todos tus recuerdos".
