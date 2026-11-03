# T13 · Foto de la cámara: "Ver", escribir y guardar (decidido por hq el 2026-11-03)

Para `solopila`. Decisión: `decisiones/2026-11-03-foto-camara-guardar.md`.
Depende de T10 (usa su editor). **Se hace en la rama `feature/T10-anotar`, después de las
pruebas finales de T10**, para unir las dos cosas a `main` de una vez.
**No cambia `docs/`** (misma regla que T10: primero se prueba).

## Por qué
La foto que se hace con la cámara de iSIMILAR solo vive en un archivo temporal: no está en la
galería. Hoy se puede ver en grande, pero no se le puede escribir ni guardar. Quien fotografía
una placa o un producto para buscar quiere a menudo quedársela o enviarla con una nota.

## Lo que cambia
1. **"Ver" junto al icono de ampliar.** En la foto base de la pantalla de resultados
   (`image_selection_view.dart`, el botón con `Icons.fullscreen_rounded`), el icono pasa a ser
   icono + texto corto ("Ver"). Mismo fondo oscuro semitransparente. Que no tape la foto más de
   lo necesario; comprobar en el Mi A3.
2. **Botones en el visor a pantalla completa** (`_showBaseImageFull`), en una barra abajo:
   - **"Escribir"**: abre el editor de T10 con la foto base. Vale para cualquier foto base, sea
     de la cámara o de la galería. Mismas reglas que T10: 1 foto al día gratis con marca de
     agua, el mismo contador, los mismos muros (`annotate_limit`, `annotate_watermark`) y solo
     se comparte, sin guardar.
   - **"Guardar"**: solo si la foto base es de la cámara. Guarda **la foto original** en la
     galería, sin texto ni marca, gratis y sin límite. Al terminar, el botón pasa a "Guardada"
     (desactivado) y sale un aviso breve. No se puede guardar dos veces la misma foto.
3. **El editor de T10 tiene que aceptar un archivo**, no solo una foto de la galería
   (`openAnnotateEditor` pide hoy un `AssetEntity`).
4. La foto base tiene que saber si viene de la cámara: hoy `ImageModel` no lo indica y las
   fotos de la galería también se copian a un archivo temporal (`home_view_model.dart`, líneas
   375, 416 y 451).

## Reglas
- **Se guarda el archivo tal cual**, sin volver a comprimirlo, con `PhotoManager.editor`.
- **La foto guardada entra en la galería** con la fecha de hoy. Comprobar si iSIMILAR la indexa
  sola o en el siguiente escaneo, y anotarlo.
- **Permisos:** en iOS, con acceso completo, guardar no pide nada nuevo. Probar con **acceso
  limitado** a las fotos. En Android 10 o superior no hace falta permiso. Si en algún caso hace
  falta uno nuevo, avisar en el buzón antes de añadirlo (cambia lo que se declara en las tiendas).
- **Relación con T12 (limpieza de la caché):** la foto de la cámara es un archivo temporal.
  La limpieza nunca puede borrar la foto base mientras se usa. Si se borra al mandar la app al
  fondo, el usuario vuelve y la foto ya no está.
- **Medición:** `actionSaveCamera = 'save_camera'` en `AnalyticsService.photoAction`, como las
  demás acciones. No hay atributo nuevo en RevenueCat.

## Textos (EN / ES / IT)
"Escribir" reutiliza `annotate_button`. Pendientes de `tono-de-marca` en hq.

| Clave | ES | EN | IT |
|---|---|---|---|
| `base_image_view` | Ver | View | Vedi |
| `camera_photo_save` | Guardar | Save | Salva |
| `camera_photo_saved` | Guardada | Saved | Salvata |
| `camera_photo_saved_toast` | Foto guardada en la galería | Photo saved to your gallery | Foto salvata nella galleria |
| `camera_photo_save_error` | No se pudo guardar la foto | Couldn't save the photo | Impossibile salvare la foto |

## Pruebas (iPhone y Mi A3)
- [ ] "Ver" se lee y no tapa la foto base; abre el visor como antes.
- [ ] Foto de la cámara: "Guardar" la deja en la galería, a resolución completa y sin marca.
      El botón pasa a "Guardada".
- [ ] Foto base de la galería: no aparece "Guardar".
- [ ] "Escribir" desde el visor: el mismo editor y las mismas reglas que T10 (límite diario, marca
      de agua, muros), con fotos de la cámara y de la galería.
- [ ] iOS con acceso limitado a las fotos: guardar funciona o avisa con claridad.
- [ ] Mandar la app al fondo y volver: la foto base sigue ahí.
- [ ] Modo avión: todo funciona.
- [ ] La foto guardada aparece después como resultado en las búsquedas.

Al terminar: informe en `docs/PARA-HQ-DE-SOLOPILA.md` con commits y lo que no se pudo probar.
