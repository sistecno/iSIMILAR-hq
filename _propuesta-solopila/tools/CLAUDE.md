# tools/ — Herramientas de modelo (Python, fuera de la app)

- `distill/` → destilación DINOv2 → MobileNetV3. **Leer `distill/ROADMAP.md` antes de nada.**
- `similarity_eval/` → harness de evaluación (917 imágenes). Es el gate de calidad:
  ningún modelo se despliega sin mAP ≥ baseline (0.790).
- No crear pipelines nuevos: reutilizar estos.
