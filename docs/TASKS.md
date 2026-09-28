# Tasks

Status: planning complete; all application implementation stages pending.

The six planning documents are present. Execute each implementation stage as BUILD → RUN → TEST → VERIFY → COMMIT → NEXT.

1. Load chosen model on CPU, inspect exact tensors, process representative screenshot crops, record recall failures.
2. Implement deterministic policies, coordinate transforms and synthetic ground truth. Verify exact strings and negative controls.
3. Decode/re-render a short silent clip with manual masks. Verify exported pixels and timing independently.
4. Connect OCR to every frame; add incomplete-processing checks. Run brief-exposure and failure-injection tests.
5. Add React review UI and local API; verify keyboard flow and offline launch.
6. On the actual HP Snapdragon machine, validate ARM64 dependencies and single-model QNN execution before integrating video. Record target-specific logs.
7. Integrate NPU pipeline, compare CPU/float/quantized variants, measure memory and end-to-end performance.
8. Package, run held-out evaluation, rehearse the honest demo and publish reproducibility notes.

**Freeze:** problem = sensitive text in short recordings; user = developer/QA author; feature = local OCR-assisted temporal review and redacted export; model = Qualcomm EasyOCR detector/recognizer; advantage = private repeated inference with measured NPU offload; architecture = React + local FastAPI + ORT/QNN + deterministic masks; demo = brief synthetic exposure found and reviewed offline. Runtime package versions, quantization and claimed performance remain validation decisions.
