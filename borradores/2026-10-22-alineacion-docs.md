# Propuesta: alinear los 3 documentos de `docs/` (contradicciones 1–4)

Estado: propuesta. Nada aplicado. Cada cambio indica el texto actual y el propuesto.
Las contradicciones 5–15 no se resuelven en los documentos (ver al final).

---

## 1. Cámara gratis o PRO
**Archivo:** `docs/guia-estrategica.md` · tabla "La web isimilar.app", fila "Gratis para siempre" (línea 178)

- Actual: `"Búsqueda desde la galería gratis; cámara y acciones en lote con PRO"`
- Propuesto: `"Búsqueda gratis para siempre; 5 búsquedas con cámara gratis; cámara ilimitada y acciones en lote con PRO"`

Motivo: el brief, la definición técnica (línea 55) y la propia guía (líneas 214, 221 y 413) dicen 5 búsquedas con cámara gratis.

## 2. "Find every photo"
**Archivo:** `docs/brief-marketing.md` · Guía para las capturas, fila 1 (línea 131)

- Actual: `"Find every photo that looks like this"`
- Propuesto: `"Find photos that look like this"`

Motivo: hasta 250 resultados y en torno al 80% de acierto (`definicion-tecnica.md`, línea 17). También cumple la regla de titulares de cinco palabras o menos.

## 3. Cloud Messaging y Remote Config
**Archivo:** `docs/definicion-tecnica.md`

3a. Tabla técnica (después de "Errores", línea 21), añadir:
```
| Notificaciones | Firebase Cloud Messaging: avisos de la app y de versiones nuevas |
| Configuración remota | Firebase Remote Config: versión mínima obligatoria (`min_build_number`, en `force_update_service.dart`) |
```

3b. Tabla "Datos y privacidad" (después de Crashlytics, línea 69), añadir:
```
| Firebase Cloud Messaging | Un token del dispositivo para enviar notificaciones; sin fotos ni contenido | Activo |
| Firebase Remote Config | Un identificador de instalación para descargar la configuración; sin fotos ni contenido | Activo |
```

Motivo: los dos están en `solopila/pubspec.yaml` (líneas 47–48) y se usan en `notification_service.dart` y `force_update_service.dart`. La política de Notion ya los declara.

## 4. Etiqueta de App Store: "no vinculados"
**Archivo:** `docs/definicion-tecnica.md` · línea 74

Apple (developer.apple.com/app-store/app-privacy-details, consultado el 22-10-2026):
> "Personal Information" and "Personal Data", as defined under relevant privacy laws, are considered linked to the user.

Para que un dato cuente como no vinculado hay que quitar antes de recogerlo identificadores como el ID de usuario. RevenueCat recibe un ID de usuario seudónimo y, según el RGPD, los datos seudónimos son personales. Conclusión probable: la etiqueta debe ser **"datos vinculados a la persona"**, sin rastreo y sin publicidad. Antes de cambiar la etiqueta, debe confirmarlo `legal-tiendas`.

- Actual: `**Etiqueta de privacidad actual en la App Store:** datos no vinculados a la persona. …`
- Propuesto: mantener la descripción de la etiqueta actual y añadir debajo:
  `**Pendiente:** según la definición de Apple, los datos personales (incluidos los seudónimos del RGPD) cuentan como vinculados. La etiqueta debe pasar a "datos vinculados a la persona", sin rastreo ni publicidad. Se cambia en App Store Connect sin enviar versión nueva.`
- Y en `guia-estrategica.md`, línea 202, cambiar "no vinculados a la persona y sin publicidad" por "sin rastreo y sin publicidad".

---

## Lo que no se arregla en los documentos
| Nº | Dónde se arregla | Quién |
|---|---|---|
| 5 Precio de respaldo $12.99 | App (`premium_service.dart`, `premium_offer_sheet.dart`) | Sesión en `solopila/` |
| 6 "From any angle" | App (`intl_en.arb:462` y traducciones) | Sesión en `solopila/` |
| 7 `firebase_analytics` en pubspec | App: quitarlo antes de la próxima versión | Sesión en `solopila/` |
| 8 "Doctors / X-rays" en la ficha | App Store Connect | `growth` redacta y Anibal lo cambia |
| 9–15 Políticas de Notion | Textos nuevos para `/privacy`, `/terms` y borrado de datos | `legal-tiendas` |
