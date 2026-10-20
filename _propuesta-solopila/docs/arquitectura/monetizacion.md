> ⚠️ Texto copiado íntegro del antiguo CLAUDE.md (oct 2026). Algunas partes están desactualizadas (créditos, versiones, dimensiones, tiempos). Ante cualquier duda manda el código; resumen vigente en `../iSIMILAR-hq/docs/definicion-tecnica.md`.


## 10. Monetización

### Modelo: Créditos + Suscripción anual + Trial de 7 días

```
PACKS DE CRÉDITOS (consumable IAP):
├── Starter:   10 créditos → $1.99
├── Pro:       50 créditos → $4.99
└── Mega:     150 créditos → $9.99

SUSCRIPCIÓN (usuarios frecuentes):
└── Anual: $19.99/año → acciones en lote ilimitadas
    └── TRIAL: 7 días gratis (introductorio) — Implementado Abr 2026

TIER GRATUITO:
├── Escanear galería completa          ✅
├── Buscar similares                   ✅
├── Ver resultados                     ✅
├── 5 búsquedas con cámara (local)     ✅
└── Borrar una por una                 ✅ siempre
```

### Implementación del Trial de 7 días (Abril 2026)

- **Configuración Nativa**: Configurado como "Introductory Offer" en App Store Connect y como "Oferta de Adquisición" en Google Play Console.
- **Detección Dinámica**: `PremiumService` detecta si el producto anual tiene un `introductoryPrice` con coste 0.
- **UI de Conversión**:
  - `PremiumOfferSheet`: El botón principal cambia dinámicamente a "Start 7-Day Free Trial".
  - `CreditsHero`: Se añadió un badge de trial ("⭐ 7 DAYS FREE") para incentivar la conversión desde Ajustes.

### Protocolo de Verificación Técnica (Play Store / App Store)

Para evitar conjeturas al implementar trials en otras apps, seguir este checklist:

1.  **Detección de Oferta**: Inyectar log en el servicio para confirmar que la tienda envía la oferta:
    `print("DEBUG: ${product.identifier} - Intro: ${product.introductoryPrice?.price}");`
2.  **Elegibilidad de Tester**: 
    - **iOS**: Resetear "Introductory Eligibility" en los ajustes de la cuenta Sandbox del dispositivo.
    - **Android**: Google Play es estricto. Si la cuenta ya usó un trial, NO lo mostrará. **Obligatorio** probar con una cuenta de Gmail "virgen" (nueva) y en modo `--profile` para ver logs.
3.  **Confirmación de Tienda**: Al iniciar la compra, el diálogo nativo (System Sheet) DEBE decir explícitamente: *"Gratis por 7 días"* o *"No se te cobrará nada hasta el [Fecha]"*. Si esto no aparece, el trial no está activo en la tienda aunque el badge de la app lo diga.
4.  **Dashboard Sync**: En RevenueCat, el producto debe mostrar "Introductory Price: Free trial" o "$0.00" tras sincronizar las credenciales de la tienda.


### Implementación con RevenueCat

- SDK: `purchases_flutter`
- Créditos = consumable IAP
- Suscripción anual = auto-renewable subscription
- RevenueCat valida compras con App Store / Google Play
- Saldo de créditos guardado localmente en `CreditEntity` (ObjectBox)
- NO construir backend de pagos propio
