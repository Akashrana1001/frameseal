# Model plan

Status: selected model family; exact runtime/precision pending validation.

| Component | Exact selection and source | Purpose and I/O | Published approximate size | Licence / target / fallback |
|---|---|---|---|---|
| Text detector | Qualcomm EasyOCR export, checkpoint `easyocr-small-stage1` | Preprocessed image to text-region evidence; CPU postprocessing produces boxes | Float detector 79.2MB, 20.8M parameters | Model card Apache-2.0; QNN HTP NPU target; same model on CPU for development where supported |
| Text recognizer | Recognizer in the same EasyOCR export | Normalized text crops to character scores; CPU decoding produces strings | Float recognizer 14.7MB, 3.84M parameters | Same card licence; QNN HTP NPU target; CPU/reference EasyOCR fallback, explicitly labelled |
| Sensitive-text policy | Original deterministic application code | Strings and boxes to candidate masks | Negligible beside models | Emails and user-supplied exact strings; no extra neural model |

The Qualcomm card provides float and w8a8 ONNX assets and X Elite NPU profiles. The listed reference image resolution is 608×800. That does not mean arbitrary video frames or crop widths are accepted; inspect the downloaded ONNX signatures and supplied preprocessing before locking tensor dimensions. Keep the recognizer's alphabet fixed to the chosen export. Model weight size is not process RAM. (see SOURCES.md)

**Path:** Qualcomm AI Hub Models / pre-exported ONNX assets → optional AI Hub Workbench compile/profile/evaluate → version-matched ONNX Runtime with QNN execution provider → QAIRT HTP backend → Hexagon NPU. Workbench is an optional online development service, not a runtime requirement; upload only synthetic calibration/evaluation examples.

The current QNN repository documents a separately registered plugin in its 2.x series. Do not combine its setup with an older bundled-provider tutorial. Native ARM64 inference and x64 export/quantization are distinct environments. Pin Python, ORT, QNN plugin, QAIRT, model checksums and target driver versions together after a successful smoke test. (see SOURCES.md)

Fixed-shape model inputs and supported operators constrain NPU execution. Use reference preprocessing, padding and bounded crop sizes; do not assume arbitrary exported PyTorch models work. Collect provider profiles and test a run that disallows CPU model fallback. CPU decoding and image processing are expected even in an NPU inference build. (see SOURCES.md)

Start with the float reference for accuracy. Test the provided w8a8 asset against the same held-out text set; select it only if sensitive-text recall remains acceptable. Do not promise a precision choice before this check. Fallback may preserve product usability, but a CPU-only finished entry would weaken the intended Snapdragon claim.

## Implementation gate

Record source URL, artifact revision/checksum, input/output names and shapes, alphabet, normalization, crop handling and licence notices. Run synthetic screenshots on CPU/reference first, then each component on the HP NPU before integrating video. If the optimized ONNX graph cannot run on CPU, use upstream EasyOCR as a reference and disclose that difference.

See [sources](SOURCES.md) for the cited evidence.
