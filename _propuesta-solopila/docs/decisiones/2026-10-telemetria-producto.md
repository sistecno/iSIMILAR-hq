# Decisión: Telemetría de producto (RevenueCat + Firebase Analytics)


### Idea registrada (Oct 2026): Telemetría de producto (RevenueCat + Firebase Analytics)
Estado: IMPLEMENTADO (medición). Pendiente: limpieza de créditos en versión aparte.

Objetivo: entender el embudo real — cuántos terminan el escaneo, cuántos llegan a una
acción en lote y qué segmento paga.

Atributos de RevenueCat (`Purchases.setAttributes`, vía `AnalyticsService`):
1. `paywall_trigger` → `camera` · `batch_delete` · `batch_album` · `settings`.
2. `batch_size` → nº de fotos seleccionadas al abrir el muro (solo cuando aplica).
3. `gallery_size` → `<3k` · `3-10k` · `>10k` (una vez: tras el escaneo o al
   arrancar si el usuario ya tenía fotos escaneadas).
4. `use_case` → `work_repair` · `work_field` · `work_creative` · `work_other` ·
   `memes_screenshots` · `everyday_photos` · `other`.

Eventos de Firebase Analytics:
`scan_started` {photo_count} · `scan_completed` {photo_count, duration_seconds} ·
`search_gallery` · `search_camera` · `photo_action` {action, photo_count, is_batch,
paywall_shown} · `paywall_shown` {trigger}.

Decisiones cerradas:
1. El evento de acciones se llama `photo_action` (no `batch_attempt`): incluye acciones
   individuales y de lote; `is_batch` distingue. `action`: `delete`, `move_album`,
   `remove_album`, `share`.
2. "Quitar de álbum" es `remove_album`, NO `move_album` (acciones distintas).
3. El valor guardado NUNCA se traduce; solo cambia el texto visible por idioma.
4. `use_case`: se pregunta una sola vez tras un cierre con éxito del muro (compra o
   inicio de prueba), nunca en "Restaurar compras", siempre con opción de omitir.
   `purchases_flutter` no expone lectura de atributos → control con flag local
   (SharedPreferences). NUNCA embeber la clave secreta de RevenueCat.
5. Privacidad (coherente con la etiqueta App Store, sin "tracking"): sin IDFA en iOS
   (`$FirebaseAnalyticsWithoutAdIdSupport`), sin Advertising ID en Android
   (`google_analytics_adid_collection_enabled=false` + `AD_ID` con `tools:node="remove"`)
   y Consent Mode con señales de publicidad denegadas (`AnalyticsService.init`).
6. La limpieza del sistema de créditos (modelo `CreditEntity`, strings y textos) va en
   OTRA versión: toca el schema de ObjectBox. Solo se renombró el botón de Ajustes
   (`get_credits` → `go_pro`, "Mejora a iSIMILAR PRO").
