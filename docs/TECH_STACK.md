# Tech stack

Planned choices; dependencies are not installed or validated by this documentation commit.

| Layer | Selection | Reason |
|---|---|---|
| UI | React + TypeScript | Timeline review and accessible controls |
| Service | Python + FastAPI | Local model integration and one worker |
| Inference | ONNX Runtime + QNN EP | Documented Qualcomm Windows route |
| Backend | QAIRT HTP | Hexagon NPU execution |
| Models | Qualcomm EasyOCR detector and recognizer | Published assets and Windows example |
| Video | Local decoder/encoder; build selected during spike | Incremental processing and silent output |
| Storage | Temporary local metadata | No server database needed |
| Evaluation | Python and synthetic fixtures | Known ground truth and failure injection |

No MongoDB, Redis, BullMQ, LangChain, hosted backend, accounts or paid model API is required.

Use an x64 development/export environment and native ARM64 inference dependencies on the HP Snapdragon target. Exact Python/ORT/QNN/QAIRT/model/driver versions will be pinned after a successful target smoke test. The current QNN 2.x plugin setup differs from older bundled-provider examples; do not mix them.

Encoder compatibility, timing preservation and redistribution licence are an implementation gate. Do not assume any arbitrary FFmpeg binary can be bundled under one universal licence. See [sources](SOURCES.md).
