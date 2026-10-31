# T9 · Textos del muro y del acordeón de inicio (decidido por hq el 2026-10-31)

Para `solopila`. Solo cambian textos en `lib/l10n/intl_{en,es,it}.arb` (y `flutter gen-l10n`).
No cambia el diseño. Revisar en pantalla que todo cabe en el iPhone y en el Mi A3; si un
texto no cabe, acortarlo en los tres idiomas igual y anotarlo en PARA-HQ-DE-SOLOPILA.

## Por qué
- **Hay textos prohibidos por el brief:** "Tiempo ahorrado: Infinito", "Encuentra cualquier
  foto al instante", "cada imagen", "Sí, siempre" (gratis a secas), "Cumplimos estrictamente
  con las directrices…".
- **Hay datos falsos:** "15.000 ≈ 2,5 min" (son unos 3,5) y "Hoy: $0.00" (en dólares para todos).
- **El muro habla de "profesionales" y de un motor**, no de lo que compra el usuario: PRO =
  cámara ilimitada + acciones en lote. Menos texto, beneficio primero, todo comprobable.

## A. Muro de pago

| Clave | ES | EN | IT |
|---|---|---|---|
| `premium_hero_title` | Borra o mueve cientos de\nfotos parecidas de una vez | Delete or move hundreds of\nsimilar photos at once | Elimina o sposta centinaia di\nfoto simili in una volta |
| `premium_hero_subtitle` | Buscar es gratis. Con PRO, la cámara no tiene límite y actúas en lote: borrar, mover a un álbum o compartir. Sin conexión: tus fotos nunca salen del teléfono. | Searching is free. With PRO, camera searches are unlimited and you act in batches: delete, move to an album or share. Works offline: your photos never leave your phone. | Cercare è gratis. Con PRO le ricerche con la fotocamera sono illimitate e agisci in blocco: elimina, sposta in un album o condividi. Funziona offline: le tue foto non lasciano mai il telefono. |
| `feature_visual_ai_title` | Cámara sin límite | Unlimited camera | Fotocamera illimitata |
| `feature_visual_ai_short` | Apunta y encuentra\nlas fotos que se parecen. | Point and find\nphotos that look alike. | Inquadra e trova\nle foto simili. |
| `feature_visual_ai_long` | Apunta la cámara a un objeto o elige una foto guardada: en menos de un segundo, iSIMILAR te enseña las fotos de tu galería que se le parecen. Sin escribir ni etiquetar. | Point the camera at an object or pick a saved photo: in under a second, iSIMILAR shows you the photos in your gallery that look like it. No typing, no tags. | Inquadra un oggetto o scegli una foto salvata: in meno di un secondo iSIMILAR ti mostra le foto della galleria che gli somigliano. Senza scrivere né etichettare. |
| `feature_bulk_cleanup_title` | Borrado en lote | Batch delete | Eliminazione in blocco |
| `feature_bulk_cleanup_short` | Selecciona todas\ny bórralas de un toque. | Select them all,\ndelete in one tap. | Selezionale tutte,\neliminale con un tocco. |
| `feature_bulk_cleanup_long` | Selecciona todas las fotos parecidas a la vez y bórralas con un solo toque, siempre con vista previa y confirmación. Libera espacio sin ir foto por foto. | Select all the similar photos at once and delete them in one tap, always with a preview and confirmation. Free up space without going photo by photo. | Seleziona tutte le foto simili insieme ed eliminale con un solo tocco, sempre con anteprima e conferma. Libera spazio senza andare foto per foto. |
| `feature_smart_organize_title` | Álbumes y compartir en lote | Albums and batch sharing | Album e condivisione in blocco |
| `feature_smart_organize_short` | Mueve o comparte\nmuchas fotos a la vez. | Move or share\nmany photos at once. | Sposta o condividi\nmolte foto insieme. |
| `feature_smart_organize_long` | Crea un álbum con tus resultados o añádelos a uno existente, y comparte muchas fotos de una vez. Agrupa por trabajo, cliente o viaje en minutos. | Create an album from your results or add them to an existing one, and share many photos at once. Group by job, client or trip in minutes. | Crea un album dai risultati o aggiungili a uno esistente, e condividi molte foto in una volta. Raggruppa per lavoro, cliente o viaggio in pochi minuti. |
| `stat_search_speed` | < 1 s | < 1 s | < 1 s |
| `stat_search_speed_label` | Por búsqueda | Per search | Per ricerca |
| `stat_offline` | 100% | 100% | 100% |
| `stat_offline_label` | Sin conexión | Offline | Offline |
| `stat_time_saved` | 0 | 0 | 0 |
| `stat_time_saved_label` | Anuncios | Ads | Pubblicità |
| `premium_free_trial_footer` | Hoy no pagas nada. Después, {fullPrice}/año. Cancela al menos 24 horas antes de que terminen los 7 días y no se te cobra. | Nothing to pay today. Then {fullPrice}/year. Cancel at least 24 hours before the 7 days end and you won't be charged. | Oggi non paghi nulla. Poi {fullPrice}/anno. Annulla almeno 24 ore prima della fine dei 7 giorni e non ti verrà addebitato nulla. |
| `unlock_everything_now` | Activar PRO | Get PRO | Attiva PRO |
| `faq_a1` | Escanear la galería, búsquedas ilimitadas desde fotos guardadas, 5 búsquedas con cámara y borrar, mover a un álbum o compartir fotos de una en una. | Scanning your gallery, unlimited searches from saved photos, 5 camera searches, and deleting, moving to an album or sharing photos one at a time. | La scansione della galleria, ricerche illimitate dalle foto salvate, 5 ricerche con la fotocamera ed eliminare, spostare in un album o condividere le foto una alla volta. |
| `faq_a2` | Búsquedas con cámara ilimitadas y acciones en lote: borrar, mover a un álbum o compartir muchas fotos de una vez. | Unlimited camera searches and batch actions: delete, move to an album or share many photos at once. | Ricerche con la fotocamera illimitate e azioni in blocco: eliminare, spostare in un album o condividere molte foto in una volta. |
| `trial_remaining` | {trial} búsquedas con cámara restantes | {trial} camera searches left | {trial} ricerche con la fotocamera rimaste |

Sin cambios: `faq_a3`–`faq_a5` (T5–T7), `less_than_coffee`, `premium_hero_badge`, cabeceras
por acción (`paywall_header_*`), textos legales y de pago.

## B. Acordeón de inicio (`home_view.dart`)

| Clave | ES | EN | IT |
|---|---|---|---|
| `hero_card_text` | Apunta la cámara a un objeto y encuentra en menos de un segundo las fotos de tu galería que se le parecen. | Point the camera at an object and find, in under a second, the photos in your gallery that look like it. | Inquadra un oggetto e trova in meno di un secondo le foto della galleria che gli somigliano. |
| `onboarding_faq_a1` | Un buscador de fotos por parecido visual. Apunta la cámara a un objeto o elige una foto guardada, y iSIMILAR te enseña las fotos de tu galería que se le parecen. Sin escribir y sin conexión. | A photo search by visual similarity. Point the camera at an object or pick a saved photo, and iSIMILAR shows you the photos in your gallery that look like it. No typing, no connection needed. | Una ricerca di foto per somiglianza visiva. Inquadra un oggetto o scegli una foto salvata e iSIMILAR ti mostra le foto della galleria che gli somigliano. Senza scrivere e senza connessione. |
| `onboarding_faq_a3` | No. El análisis se hace dentro de tu teléfono y ninguna foto sale de él. Tu galería es solo tuya. | No. The analysis happens on your phone and no photo ever leaves it. Your gallery is yours alone. | No. L'analisi avviene sul telefono e nessuna foto ne esce. La tua galleria è solo tua. |
| `onboarding_faq_a4` | Depende de tu teléfono y de cuántas fotos tengas. En un iPhone 13, 15.000 fotos tardan unos 3 minutos y medio. Solo se hace una vez: después, las fotos nuevas se analizan solas. | It depends on your phone and how many photos you have. On an iPhone 13, 15,000 photos take about 3.5 minutes. It only happens once: after that, new photos are analyzed automatically. | Dipende dal telefono e da quante foto hai. Su un iPhone 13, 15.000 foto richiedono circa 3 minuti e mezzo. Succede una sola volta: poi le foto nuove vengono analizzate da sole. |
| `onboarding_faq_a6` | Elige una foto de tu galería o haz una con la cámara: la app te enseña las que se le parecen. Luego puedes verlas, agruparlas en álbumes, compartirlas o borrar las que no necesites. | Pick a photo from your gallery or take one with the camera: the app shows you the ones that look like it. Then you can view them, group them into albums, share them or delete the ones you don't need. | Scegli una foto dalla galleria o scattane una: l'app ti mostra quelle che le somigliano. Poi puoi vederle, raggrupparle in album, condividerle o eliminare quelle che non ti servono. |
| `onboarding_faq_q7` | ¿Es gratis? | Is it free? | È gratis? |
| `onboarding_faq_a7` | Buscar es gratis para siempre: el escaneo, las búsquedas desde fotos guardadas y borrar, mover o compartir fotos de una en una. Además tienes 5 búsquedas con cámara gratis. PRO (suscripción anual con 7 días de prueba) añade cámara ilimitada y acciones en lote. | Searching is free forever: the scan, searches from saved photos, and deleting, moving or sharing photos one at a time. You also get 5 free camera searches. PRO (yearly subscription with a 7-day trial) adds unlimited camera searches and batch actions. | Cercare è gratis per sempre: la scansione, le ricerche dalle foto salvate ed eliminare, spostare o condividere le foto una alla volta. In più hai 5 ricerche con la fotocamera gratis. PRO (abbonamento annuale con 7 giorni di prova) aggiunge fotocamera illimitata e azioni in blocco. |

Sin cambios: `onboarding_faq_a2`, `onboarding_faq_a5` y las preguntas 1–6.

## Cómo medirlo
Tras publicar, comparar en RevenueCat las compras por apertura del muro con las de la versión
anterior. Si no mejora, se prueba otro titular; no cambiar varias cosas a la vez después.
