# Lyra AI — Local AI Assistant & German Language Tutor

**Status:** Lyra V1 working prototype · **German Teacher V1 core accepted: October 16, 2026** · Daily launcher improvement pending

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

## Multi-turn validation and core acceptance — October 16, 2026
A subsequent **three-turn controlled test completed all three turns**. The developer reported that the synthesized replies were understandable and accepted the audio quality.

The validation also exposed remaining issues:
- Two Teacher response/correction issues were reported in the local test summary.
- A spoken or recognized final question did not match the intended memory-recall prompt; therefore recall of the earlier person/city/day facts **was not conclusively validated**.
- A visible example of an incorrect grammar correction showed that fluent speech does **not** establish teaching accuracy.

**Updated status:** Following targeted corrections, the developer accepted the final controlled one-turn memory-recall test on October 16, 2026. The locally reported response recalled the previously supplied person, city and day, and the developer accepted voice clarity, pacing, and content. The German Teacher **V1 core feature set is closed as HUMAN PASS**, while the broader Lyra assistant remains in development. The earlier failed correction attempt remains part of the test history.

## Integration and safeguards
Local test reports describe guarded V1 integration, controlled staging runs, backup/rollback checks, preservation of existing V1 functions, and a separately isolated local model endpoint for Teacher testing so another running Ollama service need not be interrupted.

The final local handoff reported checks passing for the voice, grammar feedback, Hungarian explanation, memory recall, caption display, integrity/rollback protection, and preservation of other Lyra V1 components. The accepted speech profile is **stable_full + sampled + 1.30×**. A remaining operational limitation is that the shared Ollama endpoint does not expose the required model; the accepted testing route uses a separate isolated model endpoint, and a production one-click launcher for it is still optional/pending.

These are **locally reported development checks**, not a claim of external certification or guaranteed reliability. Sensitive local file inventories, paths, model-store contents, private recordings, and internal configuration details are intentionally excluded.


## Lyra Dev Agent 2.0 — autonomous Python development (October 16, 2026)

A separate local-first development-agent prototype reached a **three-module sandbox milestone**: Qwen2.5-Coder 14B planned and generated collaborating Python modules under `src/`; the developer's independent verification reported **3/3 files present** and **4/4 functional assertions passed**. Automatic promotion remained disabled. A subsequent test-engine milestone replaced the example-specific three-file dependency rule with **generalized explicit-dependency validation**. Focused tests covered Hungarian/English instructions, ambiguous file references, missing dependencies, and circular dependencies; the existing regression suite passed. A local checkpoint was hash-checked (15 files), with key source/backup matches confirmed. These are developer-reported tests, **not a production-ready or generally autonomous software-engineering release**.

**[Read the detailed milestone report, architecture, tests, safeguards, known limitations, and roadmap](docs/dev-agent-2-milestone-2026-10-16.md).**

## Project milestones
| Component | Status |
| --- | --- |
| Lyra V1 assistant prototype | Active development |
| German Teacher first controlled V1 microphone turn | **Milestone 1 accepted** |
| German Teacher multi-turn speech | Controlled run completed; human audio PASS |
| Grammar-correction consistency | Targeted fixes locally tested and accepted for V1 core |
| Multi-turn memory recall | Final controlled recall accepted (HUMAN PASS) |
| Reply latency optimization | Planned, non-blocking |
| Animated avatar integration | Separate ongoing work |

## Next steps
1. Optionally simplify daily startup of the isolated local model endpoint without disrupting the shared instance.
2. Improve reply latency only behind regression checks that protect the accepted speech quality.
3. Continue longer-session and background-noise reliability testing as separate follow-on work.
4. Publish additional sanitized demonstrations when approved.

## Development approach
Maintain a known-good baseline, isolate staging changes, validate installation changes against an explicit allowlist, preserve rollback options, and test independently before adopting optimizations.

## Privacy and release scope
This is a **documentation-only public showcase**. Original source code, local runtime files, model weights, API keys, secrets, private recordings, exact deployment details, and the separate Lyra V2 project are **not published**.

The project is not presented as a finished or commercially deployable product.
