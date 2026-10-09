# Skills and instruction policy — draft

## Two comparable conditions
**Baseline**: same neutral task prompt, evaluator description, tools and permitted docs; no curated language-specific skill folder. Standard installed toolchains and ordinary official documentation remain available under a controlled retrieval policy.

**Enhanced**: same task/prompt plus curated, version-pinned language-specific instructions for Rust, Scala 3, C#, Python, JavaScript/Node.js, or Java. Record each skill's title, source URL/commit, revision, file hash, commands, dependencies, and review status.

## Candidate skill areas
- Rust: Cargo, rustfmt, Clippy, async runtime, selected web framework, SQL client, tests.
- Scala 3: build tool, formatter, linter, selected HTTP/WebSocket stack, persistence and tests.
- C#: .NET SDK, formatting, analyzers, selected ASP.NET Core stack, database/test setup.
- Python: pinned Python interpreter, dependency manager, formatter/linter, ASGI framework, database adapter and tests.
- JavaScript (Node.js): pinned Node.js/runtime and package manager, formatter/linter, HTTP/WebSocket stack, database layer and tests.
- Java: pinned JDK, build tool, formatter/linter, selected backend framework, database layer and tests.

Do not present these as preinstalled. Select exact stacks during protocol review and document their versions.

## Fairness
Pack quality is a confounder; use a consistent template with similar sections (build, lint, tests, debugging, concurrency, security, DB usage). Measure and disclose instruction length and differences. Do not force equal token counts if that strips useful language-specific details; report the disparity instead. Freeze packs before a scored run and preserve them under version control.

## Trust
Treat third-party skill content as untrusted until reviewed. Reject instructions to exfiltrate secrets, alter evaluator, silently download arbitrary binaries, or bypass sandbox policies. Pin dependencies and avoid uncited claims of official endorsement.
