# Evaluation plan

| Claim | Exact measurement procedure |
|---|---|
| Finds brief sensitive exposures | Generate source clips with known synthetic text rectangles and frame ranges, including 1-, 2- and 5-frame appearances, scrolling, multiple themes and font sizes. Hold out some combinations before tuning. Count sensitive region-frame pairs not fully covered by exported opaque masks; report numerator and denominator. Separately count complete exposure events missed. |
| Preserves useful content | Measure masked nonsensitive area as a proportion of frame area; have users perform the original bug-reproduction comprehension task after redaction. Do not optimize recall by blacking out the full recording. |
| Checks all frames | Record decoded frame indices/timestamps and processing status. Require no unexplained gaps or failures. Compare input/output duration and decoded output frame sequence. This measures processing coverage, not semantic safety. |
| NPU improves performance | On the same HP PC, run identical data with equivalent model precision where supported: CPU provider and QNN HTP. Record cold start separately, warm-up then repeated runs, end-to-end completion and component p50/p95 latency. If precisions differ, report that as a confound. Keep power mode and background workload controlled. |
| Actually uses NPU | Save runtime provider/partition logs and QNN profiling output. Run a validation configuration with CPU model fallback disabled. Use Task Manager NPU graphs only as supporting evidence, not proof of graph placement. |
| Fits the device | Sample whole-process peak working set including child processes; record model files and dependency size separately. Measure maximum queue length. Vendor model memory figures are not application memory. |
| Works offline | After initial setup, disconnect network and complete import/analyze/review/export. Inspect outbound connection attempts during the run with OS networking tools; record observation scope. Zero traffic in one test is not a universal privacy proof. |
| No paid cloud inference | Inspect the shipped configuration and dependencies; show no model-service keys or inference requests. Report zero required API calls, not invented monetary savings. |
| Handles failures | Inject a model failure, a corrupted clip and cancellation. Confirm no export is enabled for incomplete processing and no original is copied to the output as a fallback. |
| Quantization is worthwhile | Compare float and w8a8 on the held-out clips using sensitive-region misses, spurious masks and end-to-end latency. Select precision based on this tradeoff. |
| Uses less energy, if tested | Use equal-work repeated runs with an external power meter where available, fixed brightness/power mode and idle baseline subtraction. Otherwise omit the energy claim; CPU load and NPU utilization are not power measurements. |

All results are pending. Publish failures as well as successes. Repository measurements should identify device SKU, Windows/driver/runtime versions, model hashes, precision, input profile and methodology. A hosted AI Hub profile can support the model choice but is not the same as measuring the HP application.
