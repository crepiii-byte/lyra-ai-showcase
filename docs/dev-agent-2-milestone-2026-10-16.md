# Lyra Dev Agent 2.0 — Autonomous Python Development Milestone

**Status:** Experimental local-first prototype  
**Documented test date:** 2026-10-16  
**Release type:** Public technical progress report; documentation only  
**Code availability:** The private local engine, generated code, credentials, and runtime configuration are not included in this showcase.

## 1. Purpose and scope

Lyra Dev Agent 2.0 is an experimental locally operated AI-assisted software-development agent. Its goal is to plan Python changes, generate and revise source files, check inter-module dependencies, run automated static/runtime checks, and keep candidate changes isolated until explicitly accepted.

This work is distinct from the Lyra V1 assistant, its German Teacher subsystem, and the separate Lyra V2 avatar project. No completed or generally reliable autonomous software engineering capability is claimed.

## 2. Demonstrated environment

The reported local development environment uses:

- **LLM:** a locally hosted Qwen2.5-Coder 14B model, served through Ollama.
- **Orchestration:** Python-based multi-file planning, generation, verification, and staged execution.
- **Host:** Windows 11 with local GPU acceleration.
- **Tests:** Python import/compile checks, lint/static-analysis tools, module-level verification, bundle/runtime checks, and independent assertions.
- **Execution separation:** a dedicated, limited Windows test account plus project-specific sandbox directories.
- **Deployment control:** automatic promotion from the sandbox into the working project was explicitly blocked in the reported acceptance runs.

The limited account and application-level path checks are safeguards, **not a guarantee of complete OS-level containment**. Generated code still requires careful review and appropriate isolation.

## 3. Workflow tested

1. Read the requested Python task and its explicit file names.
2. Generate an AI project plan with per-file responsibilities and direct `depends_on` edges.
3. Lock explicitly requested output files and validate the plan.
4. Normalize safe, unambiguous relative paths and dependency references.
5. Topologically order files so dependencies are generated before their consumers.
6. Generate each file into a staging sandbox; run individual checks.
7. Verify the complete dependency graph, imports, API contracts, and runtime bundle.
8. Obtain a project review; retain successful candidates in staging.
9. Stop before applying or promoting changes to the working project.

An invalid plan stops development before code generation. The test engine also retries planning with feedback a bounded number of times; retries do not imply that an arbitrary request can be repaired automatically.

## 4. October 16, 2026: Three-module acceptance case

### Task

Build a small coordinated Python example with:

| Module | Required behavior |
| --- | --- |
| `product_data.py` | `get_product_price(product_id)`: product 1 costs 100, product 2 costs 200 |
| `pricing.py` | `apply_discount(price, percent)`: calculate a percentage discount |
| `order_service.py` | `calculate_order_total(product_id, percent)`: use both other modules |

The requirement included `calculate_order_total(1, 20) == 80` and placing the generated modules under a `src/` directory.

### Verified dependency graph

```text
src/product_data.py ──┐
                      ├──> src/order_service.py
src/pricing.py ───────┘
```

The two underlying modules can be generated independently; the order-service module depends directly on both.

### Reported execution result

The local run reported that:

- The planner produced a valid dependency plan on its **first attempt**.
- All **three modules** were generated and passed individual checks on their **first attempt**.
- The bundle dependency, circular-import, API-contract, runtime, and project-review checks passed.
- The result was `SANDBOX_READY_NOT_PROMOTED`: candidate code remained in staging without automatic deployment.

The developer then independently executed four assertions against the generated `src` modules:

```python
assert get_product_price(1) == 100
assert get_product_price(2) == 200
assert apply_discount(100, 20) == 80
assert calculate_order_total(1, 20) == 80
```

**Acceptance result reported in the session:** `SRC_FILES_3_3_PASS`, `MULTIFILE_FUNCTIONAL_TEST_4_4_PASS`, and `SRC_MULTIFILE_ACCEPTANCE_PASS`.

This is one narrow, successful integration example with developer-reported console evidence. It is not a broad quality benchmark, third-party audit, or guarantee that arbitrary multi-file applications will work.

## 5. Defects found and fixes tested

The iterative debugging session exposed several design limitations:

| Defect | Observed symptom | Tested mitigation |
| --- | --- | --- |
| Incorrect dependency plans | Dependent module initially generated before its imports | Plan validation, dependency ordering, and bounded retry |
| Explicit-file planner bypass | Files named directly in a task were returned with empty dependencies without asking the AI | Route explicit-file tasks through AI planning while retaining a locked file list |
| AI/engine path mismatch | Model returned `src/module.py`, engine expected `module.py` | Normalize corresponding safe file and dependency paths |
| Silent dependency loss | Unknown `depends_on` entries were dropped during normalization | Preserve unknown entries so validation can reject them |
| Natural-language folder request missed | “Create these files in the src folder” generated root-level modules | Added scoped `src` destination detection and checked explicit path handling |
| Test import configuration | Independent verification initially imported from the wrong directory | Use project-root package imports for `src.*` modules |

The local test copy underwent syntax checks and focused regression checks after changes. A later test-engine update replaced the example-specific three-file dependency rule with a generalized explicit-dependency parser. The replacement passed focused contract tests and the existing regression suite; this is still limited to supported, unambiguous task phrasing.

## 6. Later October 16 update: generalized dependency validation

Following the three-module staging demonstration, the developer extended the **separate test-engine copy** with a generalized natural-language dependency checker.

The locally reported tests covered:

- Explicit relationships in supported Hungarian and English phrasings (e.g. one module uses or imports another).
- Correct interpretation of sentence boundaries without splitting `.py` file extensions.
- Safe recognition of full relative paths; ambiguous basename references are rejected instead of arbitrarily mapped to one of two same-named files.
- A limited, generalized “other two modules” reference when exactly three planned Python files are present.
- Rejection of missing required dependency edges.
- Rejection of circular dependencies, including a reverse edge added to an otherwise correctly linked three-file plan.

The example-specific `order_service.py` / `product_data.py` / `pricing.py` dependency rule was removed from the isolated **test engine**. The explicit contract test and the existing suite reported `EXPLICIT_DEPENDENCY_CONTRACT_3_3_PASS`, `DEV_AGENT_REGRESSION_PASS`, and `GENERIC_DEPENDENCY_REPLACEMENT_PASS`. An additional reverse-dependency test returned a circular-dependency error and `REVERSE_DEPENDENCY_REJECTED_PASS`.

A new local checkpoint was created. The developer reported SHA256 verification of **15 checkpoint files**, plus matching hashes for the three principal program files against the test-engine sources. This verifies the tested snapshot and selected copy matches; it does **not** constitute an independent security audit, complete reproducibility guarantee, or broad performance benchmark.

**Scope:** these were local developer-run tests, not third-party verification. The parser recognizes tested forms, not every way users might describe dependencies; larger projects, ambiguous task intent, and adversarial inputs still need more coverage.

## 7. Testing evidence and limitations

**Reported as passed:**
- Earlier isolated single-module generation and simple bug-repair experiments.
- Valid/invalid dependency-plan regression checks.
- Normalization of `src/` dependency references.
- Rejection of unknown dependency references.
- Three-file sandbox generation and bundle verification.
- Independent file-presence checks (3/3) and functional assertions (4/4).
- Promotion-blocking checks during the acceptance run.

**Not yet demonstrated comprehensively:**
- Projects with many files, multiple packages, or complex third-party dependencies.
- Robust analysis of every natural-language dependency requirement.
- Complete containment of untrusted generated code.
- Reliable unattended, long-duration operation.
- Broad regression coverage and automatic recovery for real production projects.
- General-purpose multi-project switching and management.
- A finalized user-facing monitoring/dashboard interface.

## 8. Safety and release boundaries

The work was conducted in a separate development/test setup. Safeguards reported for this setup include a limited Windows account, protected production-project areas, staged candidate files, and explicit suppression of automatic promotion.

**Important qualification:** the demonstration does not establish universal write restrictions, flawless access controls, or secure execution of arbitrary AI-generated code. Production projects should stay outside the agent's writable scope, and deployments should require a separate review-and-approval process.

This repository intentionally does **not** publish local file inventories, private paths, the development engine, checkpoint backups, runtime logs, generated private source, tokens, API keys, model files, or system account details.

## 9. Roadmap

1. Preserve the successful staging baseline as a reproducible checkpoint.
2. Convert the observed regression scenarios into durable, automated tests.
3. **Completed in the isolated test engine (tested cases):** replace the example-specific dependency rule with generalized validation; extend language and edge-case coverage.
4. Extend package and subdirectory mapping beyond the tested `src/` pattern.
5. **Next milestone:** test unfamiliar five-file and then larger multi-package tasks, starting with plan-only checks before code generation.
6. Strengthen sandbox containment, logging hygiene, auditability, and recovery.
7. Add controlled project selection, task tracking, and an operator dashboard.
8. Re-evaluate unattended autonomy only after broader correctness and safety testing.

## 10. Project status

**Milestones achieved:** creation of a small three-module Python project in isolated staging, developer-verified example behavior, and a separately tested generalized explicit-dependency validator replacing the example-specific rule in the test-engine copy.

**Overall project status:** active prototype development. This milestone does not mean Dev Agent 2.0 is complete, production-ready, or capable of safely implementing arbitrary software projects without oversight.

---

*This page documents developer-reported local test results from October 16, 2026. It is a transparent progress report, not a software release or independent certification.*
