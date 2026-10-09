# Repository-wide instructions for AI coding agents

## Goal
Design and eventually run a fair, reproducible experiment comparing AI-built Rust, Scala 3, C#, Python, JavaScript (Node.js) and Java backends. **Do not** implement a production sports community application here.

## Source of truth
Read `README.md`, `docs/experiment-protocol.md`, `docs/functional-spec.md`, `docs/evaluation.md`, `docs/cost-and-telemetry.md`, and `docs/skills-policy.md` before proposing experiments. Treat these as **draft** until the owner approves and tags a frozen protocol.

## Role handoffs
- **Research/design agent** proposes methodology; documents confounders and trade-offs.
- **Evaluator agent** owns shared tests and benchmark tooling, not language-specific solutions.
- **Implementation agent** works only in its assigned language and isolated run; cannot change contract or evaluator.
- **Reviewer agent** independently checks protocol, safety, reproducibility and interpretation.

## Rules
1. Never fabricate measurements, token counts, spending, benchmark scores, or environment access.
2. Do not modify acceptance tests to improve any candidate's score.
3. Do not let an implementation agent read other runs' code, logs, or benchmark outcomes.
4. Every run must pin model name/version where available, prompt revision, toolchain, skills, dependency lockfiles, hardware and test settings.
5. Distinguish **elapsed time**, **agent compute time**, **human time**, **tokens**, **API billed cost**, and **subscription access**. Unknown is not zero.
6. Persist raw logs only when permitted; redact secrets and personal data before publication.
7. Apply identical observable requirements and evaluator gates across languages.
8. Compilation is not acceptance; domain bugs, authorization, concurrency and delivery guarantees need independent tests.
9. Changes to experimental design require issue/PR review and must be versioned; run results belong to the protocol version used.
10. Do not install or execute unreviewed third-party skills or remote scripts; pin dependencies and document provenance.
11. Prefer narrow, verifiable incremental commits and clear issue references. Do not claim a feature works without showing the test command/result.
12. No autonomous spending, external publication, or opening broad permissions without explicit owner authorization.

## First task
Review the protocol with `prompts/codex-design-review.md`. Find missing decisions and create a concrete implementation plan. **Do not launch the main benchmark yet.**

## Benchmark coordination and preflight
Use a **Project Manager / experiment coordinator** as the default coordinating role. It tracks GitHub Issues, proposed protocol revisions, run schedules, dependencies, blockers, preflight evidence and experiment outcomes. It may coordinate setup, but must not provide different implementation advice or unplanned assistance to particular language runs. It may only launch runs if actual runner support exists; these instructions do not install an orchestrator.

Before any timed implementation run, the PM and a separate environment/setup agent must complete the reproducible environment-readiness checklist in [docs/environment-readiness.md](docs/environment-readiness.md). Preinstall and verify pinned Rust, Scala 3/JDK, .NET SDK, Python, Node.js and Java/JDK toolchains, framework prerequisites, build tools and required dependencies across equivalent isolated environments. Prepare caches/images before timing; do not charge one candidate for initial compiler/SDK installation. Record exact versions, image digests, checks, and environment differences. A failed preflight blocks the run.

**Measurement boundary:** Environment preparation and dependency provisioning are separately timed and logged as setup, not agent implementation time. Start the measured agent clock only once the specified environment and initial inputs are ready; use the same treatment for all conditions. Agents may fetch ordinary project dependencies only under a predeclared symmetric policy; record any run-time dependency downloads or tool repairs separately and mark protocol deviations. Do not silently repair only one candidate.

## Agent telemetry and audit
For each run retain a run ID, condition, assigned agent/model, prompt/skill hashes, toolchain/environment fingerprint, relevant commands, build/test outputs, errors, retries, timestamps, interventions and metric availability. Do not request or store private reasoning traces. Redact credentials and sensitive records; distinguish measured values from unavailable values. An independent reviewer checks reproducibility and isolation; PM records post-run failures and root-cause hypotheses as Issues, proposing process or skill changes **only for future versioned experimental batches**. Never modify a frozen protocol, skill set, or evaluator mid-batch to improve a candidate.

## Skills fairness
Maintain a reviewed, version-pinned skill manifest per experimental condition. Baseline runs receive no enhanced language-specific skill material; enhanced runs receive only their predefined allowed bundle. Agents may suggest new skills, but PM reviews provenance, safety and comparability and records proposals separately. No skill discovery, installation or prompt adjustment during measured runs unless explicitly included in all relevant conditions by a frozen protocol.

## Autonomous execution of approved work
When the owner requests a benchmark preparation task or approves a scoped plan, the Project Manager should execute **all authorized, unblocked steps in sequence without repeatedly asking for confirmation**. Treat approval of a defined task as permission for ordinary reversible actions within that task, such as reading repository state, creating scoped issues/branches, editing code and docs, running local scripts/tests, preparing container images with reviewed dependencies, performing preflight, collecting logs and opening PRs. Do not interpret a task as authorization to launch the main scored benchmark when the protocol is not frozen.

Standard sequence (respect actual dependencies): sync GitHub Issues, current code/branches and protocol revisions → identify outstanding decisions → prepare pinned toolchain and isolated environment → verify readiness for all six candidates → implement evaluator and runner against a frozen contract when authorized → run available smoke/CI checks → audit evidence and report outcomes. Continue through non-blocked steps even if another independent step is blocked. Parallelize independent setup/validation work only when the runner supports it, resources permit, and experiment isolation is preserved. Never assume Markdown alone creates background execution or agents.

**Ask for a decision only when genuinely required**: material protocol/framework choices not already settled, security or permission changes, purchases/paid services, publishing, deployment, external side effects, destructive/irreversible operations, unreviewed third-party code, changes to frozen acceptance tests or experimental conditions, or access/tooling failures that cannot be safely resolved inside existing authorization. Never bypass a required platform approval dialog. When blocked, log the specific blocker, carry on with permitted independent work, and present a consolidated decision request rather than interrupting for each small action.

Self-check the results of each stage and attempt bounded, reproducible corrections to ordinary build/test/setup failures. Do not alter comparison conditions or hidden evaluation criteria to achieve a pass. Record commands, changes, limitations and actual test outcomes. End with a concise completion and blocker report, not repetitive progress requests. Existing rules against automatic spending, publishing, main benchmark launches without protocol approval, and unsafe merges still apply.
