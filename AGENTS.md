# Repository-wide instructions for AI coding agents

## Goal
Design and eventually run a fair, reproducible experiment comparing AI-built Rust, Scala 3 and C# backends. **Do not** implement a production sports community application here.

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
