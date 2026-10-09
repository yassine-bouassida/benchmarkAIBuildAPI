# Cost and telemetry policy — draft

## Definitions (never conflate)
- **Tokens:** measured model input, output, and cached tokens; source and accounting semantics required.
- **API bill:** observed billed amount at published or effective rates; may include tool/model premiums; attach source.
- **Subscription:** flat access entitlement; no defensible per-run marginal cost without a declared allocation model.
- **Elapsed time:** run wall-clock time; not the same as agent compute or human time.
- **Infrastructure:** cloud machine, CI, storage and test environment costs separately measured.
- **Human intervention:** time and action recorded as a separate measure.

## Subscription-focused plan
The owner uses ChatGPT/Codex and Claude subscription interfaces, **not separately billed APIs**. Determine which executable automation and telemetry hooks the actually available Codex/Claude CLI/subscription workflows support. Do not assume agents can be programmatically launched without restrictions or that an API token counter exists. Start with a manual/semiautomated pilot and use machine-readable log output only if the installed tool provides it.

## Reporting rules
- Unavailable token data: `null`, plus `missing_reason` such as `not_exposed_by_subscription_interface`.
- Unavailable dollar data: `null`; **never zero** unless measured as truly zero billed API usage under a defined scope.
- For a subscription workflow, report plan price as a **contextual fixed monthly fee**, never as a measured per-run charge.
- Distinguish exact counters, inferred estimates, and manual records.
- Measure provider charges only with explicit credentialed account access and authorization.
- Scrub credentials and identifying traces; raw logs may require private retention.

## Instrumentation targets
run_id; language/framework; experimental condition; model and agent/CLI versions; start/end timestamps; exit/stop reason; run attempts; tool calls; token counts by category and provenance; compile/test events; commit ID; machine/container specs; peak RSS/CPU; acceptance results; measured infrastructure billing and source.

## Questions to validate in pilot
1. Does the subscription-enabled agent CLI allow noninteractive launch in the intended setup?
2. Can separate sessions be isolated with distinct working directories and state?
3. Is actual per-run token accounting exposed? What precisely do counters measure?
4. Can repeated runs continue consistently when subscription rate limits are hit?
5. Can we gather tool calls and compile failures from legitimate logs without violating privacy or usage terms?
