# Definición técnica de iSIMILAR

Actualizada el Oct 23, 2026 · @Anibal Castano

Este documento describe cómo funciona iSIMILAR hoy y qué está previsto. Es la referencia técnica del brief de marketing y de la guía estratégica: si algo de lo que se comunica no coincide con esto, manda este documento. El análisis de mercado y de clientes vive en la guía, no aquí.

## Arquitectura

iSIMILAR es un motor de búsqueda por parecido visual que funciona por completo dentro del teléfono.

| Pieza | Cómo está hecha |
| --- | --- |
| App | Flutter, publicada en iOS y Android |
| Modelo de visión | MobileNetV3-Large sin capa de clasificación (`isimilar_mobilenetv3_large_v1.tflite`, 5,7 MB). Entrada de 224×224; salida: un vector de 960 números normalizado |
| Ejecución del modelo | TensorFlow Lite en un Isolate de Dart; en Android, con aceleración por GPU (GpuDelegateV2) |
| Índice | ObjectBox con índice HNSW de 960 dimensiones |
| Búsqueda | Vecinos más cercanos por distancia euclídea sobre vectores normalizados, equivalente a la similitud del coseno. 1.000 candidatos, distancia máxima de 0,85 y hasta 250 resultados |
| Escaneo | photo\_manager genera miniaturas de 224 px; los vectores se guardan en bloques de 50 y el escaneo continúa desde el último punto |
| Almacenamiento | Solo vectores y metadatos, unos 3,84 KB por foto (10.000 fotos ocupan unos 38 MB). Los originales no se copian ni se mueven |
| Pagos | RevenueCat (purchases\_flutter 9.16.1) |
| Errores | Firebase Crashlytics |
| Analítica de uso | Firebase Analytics: preparado en el código, pero fuera de la app hasta resolver el consentimiento en la UE |

## Qué hace

1. **Escaneo inicial obligatorio.** Indexa la galería una vez, con consejos en pantalla mientras avanza. Después solo procesa los cambios.
2. **Búsqueda por foto base.** El usuario elige una foto de la galería o hace una con la cámara y recibe las fotos parecidas.
3. **Orden de los resultados.** Más parecidas, menos parecidas, más recientes o menos recientes.
4. **Detalles de cada foto.** Al abrir un resultado se ven la fecha, la resolución en píxeles y el peso del archivo.
5. **Búsqueda en cadena.** Desde cualquier resultado se puede lanzar una búsqueda nueva.
6. **Acciones sobre los resultados.** Borrar, mover a un álbum nuevo o existente y compartir: de una en una gratis, o en lote con PRO, siempre con vista previa y confirmación.
7. **Visor de álbumes.** Muestra los álbumes creados desde la app. Al abrir una foto de un álbum se ven sus detalles y se puede buscar desde ella. Las fotos que están en un álbum dejan de aparecer en búsquedas futuras. En iOS se puede quitar una foto de un álbum sin borrarla y borrar álbumes desde la app.
8. **Recordatorio semanal opcional** para revisar las fotos nuevas.

Todas estas funciones están publicadas en iOS y Android.

## Límites conocidos

- **Parecido por categoría, no por instancia.** Una placa devuelve placas en general, no la placa concreta de un cliente.
- **Funciona mejor con fotos hechas en condiciones parecidas:** misma luz, mismo fondo, mismo ángulo.
- **Precisión en torno al 80%** (mAP de 0,79 medido sobre 917 imágenes con similarity\_eval).
- **Confusión conocida:** pantallas de móvil y documentos escaneados se mezclan en alrededor de un 20% de los casos.
- **El modelo no aprende** de la galería del usuario.

## Qué no es

- No es Google Lens: no sube ninguna foto, no nombra objetos y no reconoce caras ni personas.
- No es un buscador de duplicados exactos.
- No es un organizador automático: siempre hace falta una foto base y la confirmación del usuario.
- No busca por texto, fecha, ubicación ni cliente.
- No sincroniza entre dispositivos ni tiene servidor propio.

## Modelo comercial en el código

No hay créditos a la venta. El único producto es una suscripción anual.

| Plan | Qué incluye |
| --- | --- |
| Gratis | Escaneo de la galería, búsquedas ilimitadas desde fotos guardadas, 5 búsquedas con cámara y borrar, mover a un álbum o compartir fotos de una en una |
| PRO | Suscripción anual de 12 € en la zona euro (en EE. UU., 11,99 USD; en cada país, el equivalente que fija la tienda), con 7 días de prueba. Búsquedas con cámara ilimitadas y acciones en lote: borrar, mover a un álbum o compartir muchas fotos de una vez |

**Cuándo se abre el muro de pago:** al intentar una acción en lote, al agotar las búsquedas gratuitas con cámara y desde el botón "Mejora a iSIMILAR PRO" de Ajustes. Ofrece la compra con 7 días de prueba.

**Confirmado:** las acciones en lote son siempre de PRO, sin ninguna gratuita. El aviso "5 free actions" de versiones antiguas es un resto del sistema de créditos y no debe aparecer en la app ni en las capturas de la tienda.

## Datos y privacidad

Las fotos y sus miniaturas nunca salen del teléfono. Los vectores se calculan y se guardan solo en el dispositivo.

| Servicio | Qué recibe | Estado |
| --- | --- | --- |
| RevenueCat | Compras, un identificador de usuario seudónimo y los atributos de medición | Activo |
| Firebase Crashlytics | Informes de errores | Activo |
| Firebase Cloud Messaging | Un token del dispositivo para enviar notificaciones, creado solo cuando el usuario activa el recordatorio | Activo |
| Firebase Remote Config | Un identificador de instalación para descargar la configuración remota | Activo |
| Firebase Analytics | Eventos de uso (escaneos, búsquedas, acciones, muro de pago), sin ningún contenido de las fotos | Fuera de la app hasta resolver el consentimiento |

**Configuración de Firebase Analytics:** en iOS se usa sin soporte del identificador publicitario (`$FirebaseAnalyticsWithoutAdIdSupport` en el Podfile); en Android se desactiva la recogida del identificador publicitario y se elimina el permiso `AD_ID`; el modo de consentimiento deniega las señales de publicidad y deja activa la analítica.

**Etiqueta de privacidad actual en la App Store:** datos no vinculados a la persona. Identificadores (ID de usuario e ID del dispositivo), compras, datos de uso (interacción con el producto) y diagnósticos (errores y rendimiento), usados para el funcionamiento de la app y el análisis. Sin rastreo ni publicidad.

**Decisión sobre la etiqueta (22 de octubre de 2026):** identificadores, compras, datos de uso y diagnósticos se declaran como **vinculados** a la persona, sin rastreo, porque RevenueCat usa un ID de usuario y el usuario lo envía para pedir el borrado de sus datos. Se quita "Datos de rendimiento", porque Crashlytics solo recoge errores y la app no usa Firebase Performance Monitoring. El cambio se hace en App Store Connect sin publicar una versión nueva, y hay que revisar que el formulario de Google Play diga lo mismo, incluidos Cloud Messaging y Remote Config.

**Consentimiento:** con Firebase Analytics fuera de la app y el token de notificaciones creado solo cuando el usuario activa el recordatorio, la app no necesita pedir autorización. Crashlytics y RevenueCat se explican en la política de privacidad con su base legal (interés legítimo) y la forma de oponerse: un interruptor en Ajustes, "Compartir datos técnicos para mejorar la app", activado por defecto, que desactiva Crashlytics, el envío de atributos de medición a RevenueCat y la pregunta tras la compra. Las compras siguen funcionando. Si un abogado concluye que alguno de estos datos requiere consentimiento, el interruptor tendrá que venir desactivado por defecto.

**RevenueCat sin integraciones:** comprobado el 22 de octubre de 2026, no hay ninguna integración con terceros activa (analítica, webhooks u otras). Si en el futuro se activa alguna, hay que declararla en la política y en las etiquetas. Para pedir el borrado de sus datos, el usuario copia su ID de usuario de RevenueCat desde Ajustes y lo envía por email; así se localiza al cliente sin depender del número de pedido de la tienda.

**Antes de publicar la versión con Firebase Analytics** hay que actualizar a la vez la política de privacidad, revisar la etiqueta de la App Store con la guía de declaración de datos de Firebase y actualizar el formulario de seguridad de datos de Google Play.

**Terminología:** los datos que reciben estos servicios van asociados a identificadores de usuario o de dispositivo, así que para el RGPD son datos seudónimos, no anónimos. En la política de privacidad y en cualquier texto legal nunca se escribe "anónimos". La fórmula común es "datos técnicos de compras, uso y errores, sin fotos ni contenido de la galería".

## Medición

Todo pasa por un único servicio, `lib/services/analytics_service.dart`, que nunca interrumpe el funcionamiento de la app si algo falla.

**Atributos en RevenueCat:**

| Atributo | Valores | Cuándo se guarda |
| --- | --- | --- |
| `paywall_trigger` | `camera`, `batch_delete`, `batch_album`, `settings` | Justo antes de abrir el muro de pago |
| `batch_size` | Número de fotos seleccionadas | Al abrir el muro desde una acción en lote |
| `gallery_size` | `<3k`, `3-10k`, `>10k` | Una sola vez, tras el primer escaneo |
| `use_case` | `work_repair`, `work_field`, `work_creative`, `work_other`, `memes_screenshots`, `everyday_photos`, `other` | Al responder la pregunta tras la compra o el inicio de la prueba |

**Pendiente:** compartir en lote también es de PRO, así que `paywall_trigger` necesita un valor más, `batch_share`, para cuando el muro se abre al intentar compartir varias fotos.

**Eventos en Firebase Analytics:**

| Evento | Parámetros |
| --- | --- |
| `scan_started` | `photo_count` |
| `scan_completed` | `photo_count`, `duration_seconds` |
| `search_gallery` | — |
| `search_camera` | — |
| `photo_action` | `action` (`delete`, `move_album`, `share`), `photo_count`, `is_batch`, `paywall_shown` |
| `paywall_shown` | `trigger` |
| `use_case_selected` | `use_case` |

Estos eventos están programados en `analytics_service.dart`, pero no se envían: la próxima versión se publica sin la dependencia `firebase_analytics` y con esos métodos vacíos. Mientras tanto, los datos salen solo de RevenueCat.

**Reglas de la pregunta de uso:** se muestra una sola vez, tras una compra o el inicio de la prueba, nunca al restaurar compras y siempre con opción de omitirla. Como purchases\_flutter no permite leer atributos desde la app, se recuerda con un indicador local; si el usuario reinstala, podría verla otra vez.

## Restos del sistema de créditos

El código conserva piezas de un modelo de créditos que ya no se vende. Se eliminarán en una versión separada de la de medición, porque tocar el modelo de ObjectBox puede afectar a datos guardados.

- El modelo `lib/models/credit_entity.dart` y sus referencias en `objectbox.g.dart` y `objectbox-model.json`.
- Textos de traducción sin uso, como `credits_section`, `credits_remaining`, `free_actions_label` o `annual_plan_backup_credits`.
- El widget `CreditsHero` de Ajustes: el botón ya dice "Mejora a iSIMILAR PRO", pero el nombre del widget sigue hablando de créditos.
- La sección 10 de `CLAUDE.md`, que describe paquetes de créditos y un CreditService obsoletos.
- Fuera del código, hay que comprobar que no quedan productos de créditos activos en RevenueCat, App Store Connect ni Google Play Console.

## Rendimiento medido

| Dato | Valor |
| --- | --- |
| Primer escaneo, 15.000 fotos, iPhone 13 | Entre 2,5 y 3 minutos |
| Primer escaneo, unas 8.000 fotos, Xiaomi Mi A3 (Android de gama media) | Entre 4 y 5 minutos |
| Tamaño del índice | Unos 3,84 KB por foto; unos 38 MB para 10.000 fotos |
| Precisión | mAP de 0,79 sobre 917 imágenes |
| Tiempo de búsqueda | Sin medición formal |

Mientras no se mida el tiempo de búsqueda, la comunicación dice "menos de un segundo". No se usan "50 ms" ni "0,5 segundos", y el índice no se anuncia como "23 MB".

## Hoja de ruta técnica

Nada de esto se anuncia hasta medirlo.

- **Modelo mejorado por destilación.** DINOv2 enseña a un MobileNetV3 a imitar sus vectores; en la app solo queda el modelo pequeño (unos 6 MB y unos 11 ms por foto, según el plan). Como el vector pasa de 960 a 384 números, la actualización obliga a volver a escanear todas las galerías; a cambio, el índice ocupará unos 1,5 KB por foto. Antes de publicarlo hay que comparar la precisión antes y después con el mismo conjunto de prueba.
- **Búsqueda por texto.** Prevista, sin fecha.
- **Agrupación automática sin foto base.** Idea futura, sin fecha.
- **Sincronización entre dispositivos.** No está prevista.

## Pendiente de confirmar

- [ ] Qué productos están activos en RevenueCat, App Store Connect y Google Play Console.
- [ ] Si "quitar de un álbum" se registra como `move_album` o con un valor propio (`remove_album`), como se acordó.
- [ ] Si `gallery_size` se envía también al arrancar la app para los usuarios que ya escanearon.
- [ ] Tiempo real de búsqueda.

* [ ] Qué fecha muestra el detalle de la foto y usa el orden por fecha: la de captura (datos EXIF) o la de guardado del archivo. En imágenes de WhatsApp no coinciden.
* [ ] Si `batch_size` se envía a RevenueCat: según la última revisión del código, `setAttributes` solo envía el motivo del muro, `gallery_size` y `use_case`.
