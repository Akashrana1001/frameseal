# FrameSeal: Offline Screen-Recording Redaction on Snapdragon PCs

Author: Akash (@akashrana1001)

Proposal dated 28 September 2026. Implementation and hardware validation pending.

## Concept and target users

FrameSeal is a proposed local application that finds selected sensitive text throughout short screen recordings, lets the author review redactions, and exports a processed copy without uploading the original. It targets developers and QA engineers preparing asynchronous bug reports from browsers, terminals and dashboards.

## Problem and solution

An email or private identifier can briefly appear while switching windows. Manual inspection and video masking demand attention across time; cloud processing receives the sensitive original. The user imports a supported recording, chooses email detection and optional exact private strings, then runs local analysis. Every decoded frame is processed. A timeline supports review and manual mask adjustments before exporting a separate silent video. Incomplete processing blocks export. Complete processing does not guarantee that every secret was detected.

## Innovation and alternatives

Local redaction already exists, including developer-oriented products such as Klipshot [5]. FrameSeal proposes a narrow temporal review workflow for Windows, conservative export behaviour on processing failure, public evaluation of brief exposures and measured Snapdragon NPU integration. It does not claim to invent OCR or guarantee detection of all sensitive content.

## Technical approach

React provides the review interface. FastAPI runs on loopback and coordinates a bounded worker. The CPU handles incremental video decoding, reference preprocessing, text decoding, deterministic matching and encoding. Qualcomm EasyOCR detector and recognizer ONNX models are targeted to the Hexagon NPU through ONNX Runtime QNN and QAIRT HTP. No LLM, hosted database or paid inference API is required.

## Snapdragon and Qualcomm AI Hub

Qualcomm publishes EasyOCR model assets and a Windows-on-Snapdragon example [1,2]. The selected checkpoint is easyocr-small-stage1; the card lists Apache-2.0. Exact tensor shapes, precision, runtime and driver versions will be pinned after validation. The float/reference baseline will be compared with the provided w8a8 variant. QNN profiling and a run with CPU model fallback disabled will verify NPU execution [3]. AI Hub Models and optional Workbench support artifact export, profiling and evaluation with synthetic inputs [4]; Workbench is not a runtime dependency.

## Hardware advantage to validate

Repeated visual inference is intended to run with less processing time and CPU contention on the NPU. CPU processing offers the same local privacy property. No application latency, power or battery improvement is claimed before measurement on the target Snapdragon-powered HP PC. Vendor component profiles are not end-to-end FrameSeal benchmarks.

## Deployment, accessibility and privacy

Development begins on an existing x64 laptop using CPU/reference execution; the deployment target is an HP Snapdragon Windows PC with compatible native ARM64 dependencies. Hardware access and validation are pending. A documented local launcher precedes installer work. The UI will support keyboard navigation, visible focus, labelled controls, large previews and text status beyond colour. Footage and policies stay local; logs avoid raw secrets. Original files are preserved, audio is omitted and no automatic sharing occurs. Offline use follows initial model installation.

## MVP and feasibility

The initial scope is English text, one documented 720p video profile, clips up to 30 seconds, email/exact-string rules, every-frame analysis, manual masks and silent export. Small-font OCR recall, coordinate mapping and ARM64 packaging are the main risks. Implementation progresses through CPU OCR, policy tests, deterministic video export, every-frame integration, review UI, genuine QNN deployment and held-out evaluation. Each stage is built, run, tested, verified and committed before the next.

## Demo, impact and evaluation

The proposed demo analyzes a synthetic recording offline, locates a briefly exposed identifier, supports review and exports masked video. Evaluation counts uncovered sensitive region-frame pairs and missed exposure events, including one-, two- and five-frame appearances. It also measures unnecessary masking, saved-output correctness, memory and CPU/NPU processing time on the same HP PC. Cold start and steady-state runs are separated. Energy claims require separate measurement. Intended reductions in review effort and accidental disclosure remain hypotheses for user validation.

## Current status and future scope

Current deliverables are the proposal, architecture, model plan and evaluation methodology. No application, benchmark or working demo has been completed. Later scope may include integrated capture, more text patterns, multilingual assets and an installer. Live meeting filtering, enterprise DLP and universal PII detection are excluded.

## References

- [[1] Qualcomm EasyOCR](https://huggingface.co/qualcomm/EasyOCR)
- [[2] Windows EasyOCR example](https://github.com/qualcomm/Startup-Demos/blob/main/CV_VR/AI_PC/EasyOCR/README.md)
- [[3] ONNX Runtime QNN](https://github.com/onnxruntime/onnxruntime-qnn)
- [[4] Qualcomm AI Hub Models](https://github.com/qualcomm/ai-hub-models)
- [[5] Klipshot developer workflow](https://klipshot.com/for/developers)
