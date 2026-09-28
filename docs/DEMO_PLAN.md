# Demo plan

Status: proposed walkthrough; no working demonstration currently exists.

| Time | Action | What the judge sees |
|---|---|---|
| 0:00–0:15 | Disable network connectivity; open FrameSeal | Local app loads; explain this is after installation and model download |
| 0:15–0:30 | Import a short synthetic bug recording | A terminal/browser workflow with dummy emails; a dummy identifier briefly appears during a window switch |
| 0:30–0:45 | Select email policy and enter the exact dummy identifier; click Analyze | Processing progress, distinct from the number of findings; no upload step |
| 0:45–1:15 | Open a finding and scrub its time range | Source region and proposed opaque mask; the brief exposure is visible in frame review |
| 1:15–1:35 | Add a manual mask to an intentionally unsupported item | Honest limits and useful human control |
| 1:35–2:00 | Export and open the output | Opaque masks in the saved video, original preserved, no audio track |
| 2:00–2:25 | Open measured results from the same HP machine | Actual CPU/NPU timings, processing coverage and held-out miss rate; omit unmeasured numbers |
| 2:25–2:40 | Show a pre-created failed-processing case and attempt export | Clear block rather than an unprocessed original being released |

If processing exceeds the live-demo window, show a short live clip and a clearly labelled previously measured longer run. Never present cached results as live processing. Before hardware access, any walkthrough must say CPU prototype or proposed UI; it cannot show a fabricated NPU status.
