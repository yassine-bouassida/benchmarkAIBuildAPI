# Environment readiness and measurement boundary

## Owner and timing
The Project Manager (experiment coordinator) assigns environment setup to an independent setup role **before** starting implementation agents. SDK, interpreter, compiler, runtime, framework scaffolding, approved package downloads, and image-building time count as **setup**, not measured coding-agent time. Capture setup costs separately. No agent should need to install its language toolchain during a scored run.

## Candidate preflight (pin specific versions before runs)
| Candidate | Verify ahead of time |
| --- | --- |
| Rust | `rustc --version`, `cargo --version`, required targets/tooling and build smoke test |
| Scala 3 | `java -version`, pinned `sbt --version` or selected build tool, Scala 3 compilation smoke test |
| C# / .NET | `dotnet --info`, pinned SDK and ASP.NET Core minimal startup smoke test |
| Python | `python --version`, pinned virtual environment/dependency manager, import and application startup smoke test |
| JavaScript / Node.js | `node --version`, `npm --version` or pinned selected package manager, server startup smoke test |
| Java | `java -version`, `javac -version`, pinned Maven/Gradle, compile and server startup smoke test |

For each candidate, check a shared pinned database version and connectivity, WebSocket capability, expected ports, network permissions, runtime dependencies, memory/CPU constraints, and test/evaluator access. Use the selected framework after protocol review; this checklist does **not** preselect FastAPI, Express, Spring, or another stack.

## Preflight evidence
Record and hash environment image/container/VM identifiers; OS and architecture; language, SDK, package manager, build tool and framework versions; dependencies/lockfiles; cached artifacts; command stdout/stderr and exit codes; database version; hardware/resource limits; smoke-test timestamps; network policy. Save a manifest per candidate/condition and reference it from the run record.

## Fairness and isolation
Prepare separate clean environment snapshots for each run, with equivalent resource constraints and permissions. Prewarm dependency caches using an identical declared policy, and distinguish language-specific starter differences. No implementation agent may see other solutions, logs or results. A worktree alone is not a secure isolation boundary.

If a toolchain is missing or a smoke test fails, mark environment `not-ready` and **do not begin timing**. Fix setup and re-run preflight before launch. If a measured run unexpectedly needs a new SDK/compiler, stop and record a protocol deviation; do not silently exempt installation time for only one candidate. Ordinary dependency retrieval during runs follows the same predeclared policy across languages and must be measured and disclosed if permitted.

## Freeze and review
Before the pilot/main experiment, the PM presents a preflight matrix to the independent reviewer and freezes framework choices, versions, caches, allowed docs/skills and stop rules. Setup is verified, not assumed; these are instructions, not evidence that languages are installed or automation exists.
