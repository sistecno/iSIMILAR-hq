# Destilación DINOv2 → MobileNetV3 — Plan completo


> Texto íntegro del antiguo CLAUDE.md (sección 0 "Idea registrada" + sección 17). No resumir.


### Idea registrada (Feb 2026): Destilación DINOv2 → MobileNetV3
Estado: EN EJECUCIÓN bajo control de Claude. Feedback crítico aplicado; ver sección 17.
Decisiones cerradas:
1. Se entrena directamente (sin F2 bloqueante), con Claude controlando cada artefacto.
2. Normalización ImageNet horneada en el grafo TFLite → la app sigue enviando 0–255 crudo.
3. Dataset de entrenamiento mixto: base genérica + refuerzo de categorías del producto.
4. Anti-fuga obligatorio: limpieza automática de solapamiento train/eval antes de entrenar.
Detail operativo y puntos de control: sección 17.

## 17. Destilación DINOv2 → MobileNetV3 (Roadmap operativo)

> Idea registrada Feb 2026. Estado: en ejecución bajo control de Claude.
> Reemplaza la propuesta inicial, que asumía MobileNetV3-Small/576 y partía de cero.
> Baseline real: `isimilar_mobilenetv3_large_v1` — MobileNetV3-Large, **960 dims**,
> **mAP 0.790** sobre las 917 imágenes de `tools/similarity_eval`.

### 17.1 Decisiones cerradas
1. Se entrena directamente; Claude controla cada artefacto antes de avanzar de fase.
2. Normalización ImageNet **horneada dentro del grafo TFLite** → la app sigue
   alimentando float32 crudo 0–255 (igual que hoy). El modelo es drop-in real.
3. Dataset de entrenamiento **mixto**: base genérica + sobrerrepresentación de las
   categorías del producto (boards, baterias, circuitos, pantallas, documentos, memes).
4. **Sin fuga de datos**: limpieza automática de solapamiento train/eval antes de entrenar.

### 17.2 Pipeline con puntos de control
```
F0.5  Preparación y anti-fuga            (Claude)
F1    Calibración del modelo actual      (ya existe, harness)
F2    Referencia superior DINOv2         (no bloqueante; recomendado)
F3    Pre-cálculo de targets             (Claude valida)
F4    Entrenamiento del student          (usuario ejecuta, Claude revisa)
F5    Export a TFLite FP16               (Claude valida)
F6    Gate de calidad obligatorio         (Claude)
F7    Integración Flutter + migración    (Claude)
```

- **F0.5 — Preparación y anti-fuga (Claude):**
  Inventario con SHA-256 exacto + perceptual hash (near-duplicates). Eliminar del
  train cualquier imagen que colisione con el set de eval 917. Salida:
  `manifest.json` (rutas ordenadas = índice de los targets), conteos y reporte de
  duplicados. Gate: 0 colisiones exactas y revisión manual de near-dups.
- **F2 — Referencia superior:** DINOv2-S sobre el heldout sólo como techo de
  referencia; no bloquea el entrenamiento.
- **F3 — Targets (Claude valida):** DINOv2 vits14 sobre las mismas imágenes del
  manifest, mismo preprocesado (resize directo 224, norm ImageNet, L2-norm).
  `targets.npy` float32 (N,384) alineado por índice con `manifest.json`.
  Gate: N coincide, norma L2 ≈ 1, spot-check de 20 imágenes contra el harness.
- **F4 — Entrenamiento (usuario ejecuta Colab, Claude revisa):**
  Student = MobileNetV3-Large + `projection_head` 960→384 + BN + L2-norm. Capa de
  entrada que **hornea la normalización** (x en 0–255 → `(x-mean)/std`). DataLoader
  desde el manifest, `drop_last=True` (evita BN con batch 1). Augmentation **sólo
  geométrica** (flip H, crop leve) para no romper `align_loss`. Loss híbrido
  (cosine + relacional KL). Salida: `best_student_384.pth` + `training_log.json`
  (loss y métrica de validación por época). Gate: la validación mejora y estabiliza.
- **F5 — Export (Claude valida):** `litert-torch` (NO `ai_edge_torch`, que produce
  float32). FP16 vía `TFLiteConverter` con `optimizations=[Optimize.DEFAULT]` y
  `target_spec.supported_types=[tf.float16]`. Gate de paridad: mismo input →
  `cosine(PyTorch, TFLite) > 0.999`. Verificar: input float32 0–255, output 384, ~6 MB.
- **F6 — Gate de calidad (obligatorio):** registrar el modelo en `model_registry.py`
  y correr `extract_embeddings.py` + `evaluate.py` sobre el set 917. Criterio de
  aceptación: **mAP ≥ 0.79** (baseline) y nuevo umbral euclídeo calculado.
  Si no pasa → no se despliega.
- **F7 — Integración Flutter:** `HnswIndex(dimensions: 384)` + regenerar
  `objectbox.g.dart` + schema bump + re-escaneo total. Recalibrar `maxDistance`
  (hoy 0.85 en `vector_search_service.dart`) con el `euclidean_equiv` del harness.
  Actualizar localizaciones "960-dimensional" → 384. `min_build_number` forzado.
  Actualizar este `CLAUDE.md`.

### 17.3 Correcciones respecto a la propuesta original
- El modelo actual NO es Small/576: es **Large/960** (este documento estaba desactualizado).
- El destilado **no es drop-in** salvo que se hornee la normalización en el grafo.
- Faltaba criterio de aceptación medible → mAP ≥ baseline en el harness existente.
- Faltaba anti-fuga y manifest alineado → un desalineamiento de índice arruina todo.
- La conversión FP16 descrita era incorrecta (`ai_edge_torch` es float32; usar `litert-torch`).
- Augmentation vs. targets congelados: sólo geométrica.
- Reutilizar `tools/similarity_eval/`, no crear un pipeline nuevo.
