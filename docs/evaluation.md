# Evaluation plan — draft

## Correctness gates (independent evaluator)
1. Builds, starts and responds according to contract.
2. Runs migrations and persists/retrieves data.
3. Rejects unauthorized cross-group access and improper role grants.
4. Handles simultaneous last-seat registrations without overbooking.
5. Maintains deterministic FIFO fairness under contention and timestamp ties.
6. Performs offer/accept/expire transitions atomically and idempotently.
7. Delivers persisted messages to current clients, supports reconnection and history.
8. Produces correct recipient-scoped cancellation and promotion notifications.
9. Recovers after process restarts without lost committed message/notification intent.
10. Rejects malformed inputs, duplicate commands, and illegal state transitions.

Report each case as PASS, FAIL, ERROR, or NOT_RUN; do not count NOT_RUN as PASS.

## Runtime metrics
- Request and message latency: p50, p95, p99.
- Throughput, failure rate, dropped/duplicated messages, delivery delay.
- Concurrent WebSocket connection success and reconnect behavior.
- CPU time/usage, peak RSS, network and database resource use.
- Warmup, dataset cardinality, request mix, payload size and test duration.

Performance numbers only for implementations satisfying a minimum correctness threshold, with failures shown explicitly. Use a fixed load-generator implementation that is not being benchmarked. Benchmark one candidate at a time on matching hardware with controlled DB state.

## Development metrics
- End-to-end wall-clock duration, actual active agent time if observable.
- Number of tool calls, compile attempts, failing/passing test cycles.
- Input/output/cached tokens *only when instrumented and trustworthy*.
- Human interventions, dependencies downloaded, test modifications, agent retries.
- Completed user stories and acceptance coverage.
- Security/maintainability review findings with consistent rubric.

## Analysis
Compare success rates and distributions across repeated runs; include uncertainty and outliers. No unqualified claim that a language intrinsically 'wins'. Avoid a single weighted score without pre-registered weights and sensitivity analysis.

## Implementation milestones
- P0: evaluator contract + fixtures + smoke tests.
- P1: concurrency/security functional suite.
- P2: messaging reconnect/failure suite.
- P3: telemetry/runner verification.
- P4: load harness and publication report generation.
