---
name: checklist-release
description: Lista de comprobación antes de publicar una versión de iSIMILAR en App Store o Google Play, o un cambio en la web. Úsala antes de enviar a revisión, al cambiar precios o pruebas, o al añadir un servicio que recoge datos.
---

# Checklist de publicación

Marca cada punto como hecho / no aplica / pendiente, con la evidencia.

## Versión de la app
- [ ] Número de versión y build actualizados en `../solopila/pubspec.yaml`.
- [ ] Notas de la versión en EN, ES e IT.
- [ ] Textos nuevos traducidos en `lib/l10n/intl_{en,es,it}.arb`.
- [ ] Ningún resto de créditos visible ("5 free actions", créditos restantes).
- [ ] Probado en un iPhone y un Android reales, incluido el escaneo inicial.
- [ ] Si cambia el esquema de ObjectBox o el modelo: migración probada sobre una
      galería ya escaneada, y plan de re-escaneo comunicado.
- [ ] Tras publicar: subir `min_build_number` en Firebase Remote Config si la
      versión anterior debe dejar de usarse.

## Datos y privacidad (si cambia lo que se recoge)
- [ ] Política de privacidad actualizada y publicada en su URL.
- [ ] Etiqueta de privacidad de App Store revisada.
- [ ] Formulario de seguridad de datos de Google Play actualizado.
- [ ] Los tres cambios se hacen a la vez que la versión, no después.
- [ ] Pasar el agente `legal-tiendas`.

## Suscripción y prueba gratuita
- [ ] Precio, duración y prueba claros en el muro; botón "Restaurar compras";
      enlaces a términos y privacidad.
- [ ] Precio idéntico en app, ficha de tienda, web y anuncios (skill `tono-de-marca`).

### Protocolo de verificación del trial (copiado de ../solopila/docs/arquitectura/monetizacion.md)

Para evitar conjeturas al implementar trials en otras apps, seguir este checklist:

1.  **Detección de Oferta**: Inyectar log en el servicio para confirmar que la tienda envía la oferta:
    `print("DEBUG: ${product.identifier} - Intro: ${product.introductoryPrice?.price}");`
2.  **Elegibilidad de Tester**: 
    - **iOS**: Resetear "Introductory Eligibility" en los ajustes de la cuenta Sandbox del dispositivo.
    - **Android**: Google Play es estricto. Si la cuenta ya usó un trial, NO lo mostrará. **Obligatorio** probar con una cuenta de Gmail "virgen" (nueva) y en modo `--profile` para ver logs.
3.  **Confirmación de Tienda**: Al iniciar la compra, el diálogo nativo (System Sheet) DEBE decir explícitamente: *"Gratis por 7 días"* o *"No se te cobrará nada hasta el [Fecha]"*. Si esto no aparece, el trial no está activo en la tienda aunque el badge de la app lo diga.
4.  **Dashboard Sync**: En RevenueCat, el producto debe mostrar "Introductory Price: Free trial" o "$0.00" tras sincronizar las credenciales de la tienda.



## Ficha de tienda y web
- [ ] Capturas según la guía del brief (resultado, no proceso; ≤5 palabras por titular).
- [ ] La web (`../solopila_landingPAGE/web/`) coincide con la versión publicada:
      funciones, precio y enlaces a App Store y Google Play.
- [ ] Commit en git de la app y de la web antes de publicar.
