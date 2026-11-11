# Próxima versión · foto buscada, álbumes y compartir hacia iSIMILAR (2026-11-11)

Origen: preguntas de Anibal al hacer las capturas. Datos del código de `solopila`
(rama `fix/T14-T15`, solo lectura). Nada de esto entra en la versión que se compila ahora.

## T17 · La foto buscada debe salir siempre la primera
**Hoy:** nada lo garantiza (`vector_search_service.dart:13-30`, `home_view_model.dart:456-489`).
- Elegir desde la galería usa `image_picker`: devuelve un archivo temporal sin el id de la foto.
  El vector se calcula en el momento y se busca en el índice.
- Si la foto **no está escaneada**, no está en el índice y no sale. (Anibal acertó.)
- Si está **en un álbum de la app**, se excluye (`!isInAlbum`).
- Aunque esté escaneada, el escaneo usa la miniatura 224×224 y la búsqueda el archivo completo:
  suele salir arriba, pero puede ganarle una ráfaga o un duplicado.
- "Buscar similares" desde un resultado sí reutiliza el vector guardado: sale primera.
- Cámara: la foto no está en la galería, así que nunca sale en resultados (solo arriba).

**Qué pedir:** que, al buscar desde la galería, la foto elegida sea el resultado 1 cuando esté
en la galería, también si no está escaneada o está en un álbum. Exige conocer su id (cambiar
el selector por uno de `photo_manager`, o buscar el id). A decidir por `solopila`.

## T18 · Orden de las fotos dentro del álbum
**Hoy:**
- iOS: las más recientes en añadirse, primero. Con "Seleccionar todo" se añaden en orden de
  parecido, así que **la menos parecida sale la primera** (inferido del código de photo_manager;
  sin probar en el iPhone).
- Android: orden del escaneo (`objectbox_service.dart:84-86`).
**Qué pedir:** mismo orden que los resultados de los que salió el álbum, en las dos plataformas.

## T19 · Ordenar dentro del álbum
- Más recientes / más antiguas: fácil (`createDateTime` ya está disponible).
- Más / menos parecidas: el álbum no guarda la foto buscada (`album_entity.dart` solo tiene id,
  nombre y fecha). Haría falta guardar el vector de la foto buscada al crear el álbum.

## T20 · iSIMILAR en el menú "Compartir" de otras apps
Compartir una foto desde Fotos, WhatsApp o Gmail hacia iSIMILAR y que se busque con ella.
**Hoy no existe nada** (sin extensión de iOS ni `intent-filter` en Android).
- Android: un `intent-filter` `ACTION_SEND` `image/*`. Poco trabajo.
- iOS: una Share Extension, App Group, esquema de URL y un paquete (`receive_sharing_intent`
  o `share_handler`). Trabajo medio y prueba en dispositivo.
- Se reutiliza `searchSimilar()` separándolo en `searchSimilarFromFile(File)`.
- Revisar con `legal-tiendas`: no recoge datos nuevos, pero la etiqueta de la App Store y el
  texto de la ficha pueden mencionarlo.

## T21 · Avisos raros vistos en las capturas (inglés, 2026-11-11)
- Tras mover las 250 fotos a un álbum, la lista queda en "0 results" con el mensaje "Sorry, some
  photos do not have the necessary quality to be classified". El mensaje es falso en ese caso:
  las fotos no faltan por calidad, se fueron al álbum.
- ~~250 en el aviso y 247 en el álbum~~: no es un fallo. Anibal borró 3 falsos positivos que, por
  el orden de T18, salían los primeros del álbum.

**Decisión (Anibal, 2026-11-11):** T17–T21 van todas a la próxima versión.
