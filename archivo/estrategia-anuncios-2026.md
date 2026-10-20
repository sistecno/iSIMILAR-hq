# Estrategia de Anuncios (Paid Acquisition)

> Documento de trabajo. Captura el dilema del SDK de Meta y las alternativas
> sin comprometer la propuesta de valor (privacidad, 100% offline).
> Última actualización: Septiembre 2026

---

## 1. Objetivo

Adquirir usuarios para iSIMILAR en App Store / Google Play sin romper el
pilar de marca: las fotos nunca salen del dispositivo.

---

## 2. El dilema

Premisa a evaluar:

> "Para poder publicitar la app tenemos que instalar un SDK de Meta."

**Esto no es una regla absoluta.** Se puede enviar tráfico a la ficha de la
tienda sin instalar ningún SDK. Lo que sí exige el SDK de Meta (o un MMP de
por medio) es la **atribución fiable de instalaciones** y la **optimización
por eventos dentro de la app** (trial iniciado, suscripción comprada).

La pregunta correcta no es "¿hay que instalarlo?" sino "¿cuánta precisión de
medición necesito y cuánto me cuesta en privacidad?".

---

## 3. Qué habilita el SDK y cuándo es realmente necesario

| Objetivo de campaña | ¿Requiere SDK de Meta? |
|---|---|
| Tráfico / alcance a la ficha de tienda (sin optimización) | No |
| Instalaciones con atribución precisa | Sí, o MMP (AppsFlyer/Adjust/Branch) |
| Optimización por eventos in-app (trial, compra) | Sí, o MMP |
| Públicos personalizados / lookalike por eventos | Sí, o MMP |
| Retargeting de usuarios de la app | Sí, o MMP |

Notas por plataforma:

- **iOS:** la atribución de installs va por **SKAdNetwork**. El SDK de Meta
  facilita el manejo del *conversion value* y el prompt ATT, pero no es la
  única vía (se puede implementar SKAN nativo o vía MMP).
- **Android:** Meta soporta el *install referrer* de Google Play; el SDK
  añade los eventos in-app y la optimización.

> Verificar requisitos exactos en la documentación oficial de Meta antes de
> ejecutar: las reglas de atribución y SKAN cambian con frecuencia.

---

## 4. Coste real de meterlo (y por qué choca con el producto)

- **ATT en iOS** + etiqueta "Datos usados para rastrearte" en la ficha de App Store.
- **Data Safety** en Play declarando identificadores compartidos con terceros.
- **GDPR / consentimiento** en los mercados actuales de la UE (ES, IT).
- **Contradicción de marca:** el pilar #1 es "100% offline y privado". El SDK
  no lee fotos, pero sí envía identificadores de dispositivo y eventos a Meta.
  Un usuario o un revisor puede señalarlo.
- **Revisión de App Store** más estricta al declarar tracking.

---

## 5. Alternativas sin SDK de Meta

| Canal | SDK de terceros | Encaje con privacidad | Notas |
|---|---|---|---|
| Apple Search Ads | No | Alto | Intención alta ("photo finder", "duplicate cleaner"); atribución de Apple. Solo iOS. |
| Google App Campaigns | No (usa Firebase) | Medio-alto | Ya existe Firebase; falta `firebase_analytics` y link a Google Ads. Android + iOS. |
| Orgánico TikTok/Reels/Shorts | No | Alto | Ya definido en `iSIMILAR_BRIEFING.md` secc. 9. |
| Influencers del nicho técnico | No | Alto | Alineado con el público blue-collar. |
| Meta (solo tráfico/boost a la ficha) | No | Medio | Medición pobre y sin optimización por eventos. |

---

## 6. Embudo con el sitio web como intermedio

Funnel: anuncio → `isimilar.app` → botón tienda → App Store/Play → install →
abrir → trial/compra.

Estado del sitio (revisado Sept 2026): landing con links directos a ambas
tiendas, CTA "Probar 7 días gratis" y QR. **No tiene píxel ni analítica
instalada** (ni Meta Pixel, ni GA4/GTM). Hoy no se puede medir ni retargetear
nada desde el sitio.

### Cómo afecta a la conversión

- Cada paso extra es una caída. Un embudo web suele convertir peor que una
  campaña de instalación directa a la tienda: el usuario debe (1) entrar al
  sitio, (2) tocar "descargar", (3) descargar, (4) abrir. Más fricción, menos
  conversión.
- A cambio: control del mensaje, credibilidad, SEO y público de retargeting.
- El número real no se adivina: hay que testear A/B (directo a tienda vs web).

### Qué se puede medir y qué no (web intermedio)

| Etapa | ¿Medible sin SDK en la app? | Cómo |
|---|---|---|
| Visita al sitio | Sí | Meta Pixel / Conversions API |
| Clic al botón de tienda | Sí | Pixel (evento custom) |
| Instalación | Parcial | SKAdNetwork (iOS, agregado y con retraso); Play Install Referrer (Android) |
| Trial / suscripción | No con precisión | Apps nativas de tienda / RevenueCat |

Punto clave: el píxel web **no ve** la instalación ni la compra. Hay un hueco
entre "clic a la tienda" y "suscripción".

### ¿Medir ayuda a optimizar?

Sí, pero solo si mides el evento correcto:

- Si optimizas por "clic al botón", Meta buscará gente que hace clic barato, no
  necesariamente gente que instala y paga (trampa del proxy).
- Cuanto más cerca esté el evento optimizado del resultado de negocio (compra),
  mejor la eficiencia. Pero Meta necesita volumen (~50 eventos/semana por
  conjunto) para salir de la fase de aprendizaje; una app nueva rara vez tiene
  suficientes compras.
- Camino sin SDK en la app para eventos reales: **Google App Campaigns**
  (Firebase) y **Apple Search Ads** miden instalación/compra con sus propias
  herramientas. Para que Meta optimice por trial/compra habría que revisar la
  integración **RevenueCat → Meta (Conversions API)** y verificar si exige un
  identificador que hoy solo da el SDK en la app.

---

## 7. Recomendación (a validar)

**No meter el SDK de Meta en la app principal por ahora.** Arrancar con:

1. **Apple Search Ads** (iOS) — sin SDK, alineado con la marca.
2. **Google App Campaigns** — aprovechando la infraestructura Firebase ya
   presente (añadir Firebase Analytics + link a Google Ads).
3. **Orgánico** (TikTok/Reels/Shorts + Reddit), ya planificado.

Razones:

- Preserva la etiqueta de privacidad y evita pedir permiso de tracking para
  algo que el producto promete no hacer.
- Aprovecha infraestructura que ya está en el proyecto.
- Meta no se descarta para siempre; se reevalúa solo si ASA/UAC no escalan, y
  en ese caso se decide entre MMP o campañas sin optimización.

---

## 8. Decisión (pendiente de confirmar)

- [ ] ¿Se descarta Meta Ads por ahora?
- [ ] ¿Se activa Firebase Analytics para Google App Campaigns?
- [ ] ¿Presupuesto y mercados iniciales?

---

## 9. Preguntas abiertas

- ¿La atribución sin SDK en Meta basta para las metas de adquisición, o el
  producto necesita optimizar por compra/trial desde el día uno?
- ¿Vale la pena un MMP (que igualmente añade tracking) o es preferible
  mantener la app limpia y medir con las herramientas nativas de cada tienda?
- ¿El público objetivo (técnicos, blue-collar) se adquiere mejor por Meta o
  por Apple Search Ads / Google App Campaigns?
