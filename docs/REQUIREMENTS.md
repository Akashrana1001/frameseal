# Requirements

Status: proposed MVP, 28 September 2026.

**Problem:** A developer records a bug reproduction in a browser, terminal or dashboard. An email address, account identifier or credential-like string appears while switching windows. Manually scanning a recording is tedious, while a cloud redaction workflow receives the sensitive original. This is a concrete risk scenario; we have not measured its prevalence. Validate with three to five developers before making adoption or time-saved claims.

**Primary user:** an individual developer or QA engineer preparing a short asynchronous bug report. Initial domain: English, visibly readable text in a 720p desktop recording.

**Core feature:** import a short recording, detect selected sensitive text locally, review time-indexed opaque masks and export a new silent video. The original stays unchanged.

1. Open the locally served application and import a supported clip.
2. Choose the email rule and optionally supply exact private strings. Use only synthetic values in the demonstration.
3. Click Analyze. Decode every frame, run OCR, map detected text to original coordinates, apply deterministic rules and build a review timeline. Show progress and processing failures separately from detected content.
4. Review flagged time spans. Add, adjust or remove masks. Unreadable text candidates can be flagged, but completely missed text cannot automatically be classified as uncertain.
5. Click Export after review. Re-render each frame with opaque rectangles, omit audio and unnecessary metadata, and write a separate output. Failed decoding, model execution or incomplete processing blocks export.
6. Open the exported file for a final review and clear temporary analysis data.

**Critical distinction:** complete frame processing does not prove complete sensitive-content detection. Never display “100% safe” or issue a security certification. A missed OCR region can still escape detection; manual review remains part of the product.

**Must build:** one supported 720p MP4 input profile, clips up to 30 seconds; English OCR; email and exact-string rules; all decoded frames processed; time-indexed review; manual masks over selected time spans; opaque-mask export with audio removed; processing-error export block; offline operation; CPU baseline and later genuine QNN execution; synthetic test clips and measurements.

The demo source can use readable text and a documented capture profile. Do not downsample frame rate to hide difficult exposures. Reject unsupported streams explicitly. Preserve temporal ordering; validation must compare the exported decoded frames, not only in-memory masks.

**Should build:** mask persistence across adjacent frames, configurable spatial padding, unreadable-candidate indicators, an export report with counts rather than raw secrets, keyboard review shortcuts, float-versus-quantized evaluation.

**Only if time remains:** capture within the app, additional credential formats, multilingual recognition, installer, longer recordings, optional speech redaction with a separately validated model.

**Outside scope:** live Zoom/Teams filtering, screen streaming, a system-wide DLP agent, LLM-based semantic PII detection, autonomous sharing, medical or legal compliance claims, guaranteed identification of all secrets.

The toughest constraint is **OCR recall at the actual text scale**, compounded by recognition work per detected region. Detector latency alone cannot predict full-video speed. If readable-text accuracy is poor, fix preprocessing/tile strategy or reduce the supported capture profile before adding features. Do not conceal missed detections behind manual-only curated demonstrations.

## Acceptance criteria

- Supported input profile loads; unsupported duration, resolution or encoding is rejected clearly.
- Frame index/timestamp ledger has no unexplained gaps; zero findings is not a safety guarantee.
- Known text-region rectangles remain correctly covered after preprocessing coordinate transforms.
- User can add, adjust and remove spatial and temporal masks with labelled controls.
- Independently decoded export has expected opaque masks, no audio and correct temporal order.
- Original file hash remains unchanged.
- Decode/model failure or cancellation prevents successful export; no original-copy fallback.
- After setup, the full workflow completes offline.
- Actual HP NPU execution is verified; CPU fallback is identified accurately.

Numeric accuracy and speed targets will be set after the baseline rather than fabricated for the proposal.
