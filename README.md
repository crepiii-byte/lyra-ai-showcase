# Lyra AI — Local AI Assistant & German Language Tutor

**Status:** Working prototype · **German Teacher Milestone 1 accepted: October 15, 2026** · Multi-turn validation in progress (October 16, 2026)

Lyra V1 is an experimental local-first AI assistant exploring Python automation, locally hosted language models, speech interfaces, Windows controller integration, and smart-home systems.

## Technology
Python · Ollama · Coqui XTTS · Speech recognition · PowerShell · Windows · Home Assistant · ESP32 / ESPHome

## Capabilities under development
- Local AI-assisted conversation and task orchestration.
- Speech recognition and synthetic speech.
- Home Assistant and IoT integrations.
- German-language tutoring with grammatical feedback and Hungarian explanations.
- Controlled software deployment, backup, rollback, and regression testing.

## German Teacher — Milestone 1 accepted
A controlled **single-turn V1 microphone test** was completed and accepted by the developer on October 15, 2026.

- Recognized a spoken German sentence.
- Corrected **"Dieses Satz" → "Dieser Satz"**, with a Hungarian grammar explanation.
- Provided a contextual German follow-up.
- Produced understandable German speech using the accepted **1.30× Coqui XTTS profile**.
- Displayed the speech-recognition transcript, Teacher text, and synthesized reply in a diagnostic caption view.

**Locally reported first-test measurements**

| Metric | Result |
| --- | --- |
| First audible output | ~15.68 seconds after speech ended |
| Complete spoken reply | ~20.62 seconds |
| Speech/audio text consistency | Reported PASS |
| Human listening assessment | Accepted |

These are measurements from a locally reported controlled test, **not independently verified production benchmarks**.

## Multi-turn validation — October 16, 2026
A subsequent **three-turn controlled test completed all three turns**. The developer reported that the synthesized replies were understandable and accepted the audio quality.

The validation also exposed remaining issues:
- Two Teacher response/correction issues were reported in the local test summary.
- A spoken or recognized final question did not match the intended memory-recall prompt; therefore recall of the earlier person/city/day facts **was not conclusively validated**.
- A visible example of an incorrect grammar correction showed that fluent speech does **not** establish teaching accuracy.

**Status:** Audio quality accepted for this test; grammar-correction reliability and multi-turn memory acceptance remain **pending**. The project is **not declared complete**.

## Integration and safeguards
Local test reports describe guarded V1 integration, controlled staging runs, backup/rollback checks, preservation of existing V1 functions, and a separately isolated local model endpoint for Teacher testing so another running Ollama service need not be interrupted.

These are **locally reported development checks**, not a claim of external certification or guaranteed reliability. Sensitive local file inventories, paths, model-store contents, private recordings, and internal configuration details are intentionally excluded.

## Project milestones
| Component | Status |
| --- | --- |
| Lyra V1 assistant prototype | Active development |
| German Teacher first controlled V1 microphone turn | **Milestone 1 accepted** |
| German Teacher multi-turn speech | Three-turn controlled run completed; audio accepted |
| Grammar-correction consistency | Further validation/fixes pending |
| Multi-turn memory recall | Final acceptance pending |
| Reply latency optimization | Planned, non-blocking |
| Animated avatar integration | Separate ongoing work |

## Next steps
1. Diagnose and resolve the specifically observed Teacher corrections without changing the accepted speech chain.
2. Verify multi-turn recall in a controlled, clearly prompted follow-up.
3. Recheck regression and rollback safeguards after any targeted correction.
4. Update this public showcase only when results are confirmed.

## Development approach
Maintain a known-good baseline, isolate staging changes, validate installation changes against an explicit allowlist, preserve rollback options, and test independently before adopting optimizations.

## Privacy and release scope
This is a **documentation-only public showcase**. Original source code, local runtime files, model weights, API keys, secrets, private recordings, exact deployment details, and the separate Lyra V2 project are **not published**.

The project is not presented as a finished or commercially deployable product.
