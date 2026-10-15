# Lyra AI — Local AI Assistant & German Language Tutor

**Status:** Working prototype · **Milestone 1 completed: October 15, 2026** · Development ongoing

Lyra V1 is an experimental local-first AI assistant exploring Python automation, locally hosted language models, speech interfaces, Windows controller integration, and smart-home systems.

## Technology
Python · Ollama · Coqui XTTS · Speech recognition · PowerShell · Windows · Home Assistant · ESP32 / ESPHome

## Capabilities under development
- Local AI-assisted conversation and task orchestration.
- Speech recognition and synthetic speech.
- Home Assistant and IoT integrations.
- German-language tutoring with grammatical feedback and Hungarian explanations.
- Controlled software deployment, backup and regression testing.

## German Teacher — Milestone 1 Complete
A controlled **single-turn live microphone test** was completed on October 15, 2026.

- The system recognized a German sentence spoken into a microphone.
- It corrected the intentional grammatical error **"Dieses Satz" → "Dieser Satz"**.
- It supplied a Hungarian explanation and a contextual German follow-up question.
- It generated German speech using the accepted **1.30× Coqui XTTS profile**.
- The developer confirmed that the spoken output was satisfactory.

**Recorded first-test performance**

| Metric | Result |
| --- | --- |
| First audible output | ~15.68 seconds after speech ended |
| Complete spoken reply | ~20.62 seconds |
| Speech/audio text consistency | Reported PASS |
| One-turn user listening test | Accepted |

These are results from one locally reported controlled test, **not production benchmarks**. Multi-turn reliability, background noise handling and latency improvements remain to be tested.

## Project milestones
| Component | Status |
| --- | --- |
| Lyra V1 assistant prototype | Active development |
| German Teacher controlled deployment | Completed |
| German Teacher first microphone turn | **Milestone 1 completed** |
| Reply latency optimization | Planned |
| Extended teaching sessions | Not yet verified |
| Animated avatar integration | Separate ongoing work |

## Development approach
Maintain a known-good baseline, isolate staging changes, validate installation changes against an explicit allowlist, preserve rollback options, and test independently before adopting optimizations.

## Next steps
1. Reduce first-audio latency while preserving speech quality.
2. Expand to multi-turn German teaching.
3. Test robustness in the presence of background television/noise.
4. Publish additional sanitized demonstrations.

## Privacy and release scope
This is a **documentation-only public showcase**. Original source code, local runtime files, model weights, API keys, secrets, private recordings, exact deployment details, and the separate Lyra V2 project are **not published**.

The project is not presented as a finished or commercially deployable product.
