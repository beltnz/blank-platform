# DEVELOPMENT, TEST DATA & VERIFICATION MODEL
## Blank Production Application Platform — Version 0.02.0

# 1. Objective

Provide fast, deterministic, safe development and proportionate verification without weakening release confidence or exposing production data/powers.

# 2. Trusted Environments

Conceptual environments: `development`, `test`, `staging`, `production`. Identity comes from trusted deployment/runtime configuration, never client input. Environment policy itself should be testable.

Production defaults:

- no reset/truncate/test-data generation;
- no local fake-provider fallback;
- no direct SQL by default;
- restricted Data Inspector;
- non-verbose public errors;
- production-only secrets/data separation.

# 3. Data Operations

Provide deterministic, documented operations as applicable:

- Seed baseline;
- Generate/populate empty;
- Append;
- Reset;
- Clear eligible data;
- Load/Rebuild named scenario;
- Restore baseline.

A developer should not need undocumented SQL to recover local state. Destructive commands clearly show target environment/database/tenant and use stronger confirmation outside disposable environments.

# 4. Synthetic Data

Synthetic data is default outside production. Production-derived data requires explicit masking/protection policy. Fixtures that look sensitive are clearly synthetic. Test credentials/keys cannot authenticate to production.

# 5. Factories, Fixtures and Scenarios

Factories produce valid defaults and controllable edge/pathological states. Named scenarios are version-controlled, reproducible and record random seed when relevant. Promote repeatedly useful ad-hoc setup into a named fixture; remove stale fixtures.

# 6. Protected System State

Protect invariants, not magic IDs. Examples: at least one viable recovery administrator, active required keys/config, migration history. Reset/clear must preserve or recreate minimum operable state.

# 7. Fake Providers and Determinism

Development/test may use fake email/SMS/storage/payment/etc. sinks, controllable clock/random and failure injection. Fakes cannot silently replace failed production providers. Most tests should avoid paid/rate-limited external sandboxes.

# 8. Verification Portfolio

Use the cheapest test capable of proving the requirement:

- unit — isolated behaviour;
- contract — public capability semantics;
- integration — database/queue/storage/provider boundaries;
- E2E — critical user workflow;
- security — auth/authz/tenant/admin/input/failure;
- architecture fitness — dependency and structural invariants;
- operational — migration/backup/restore/deploy/health.

Coverage percentage is not contract evidence.

# 9. Risk Tiers

- **T0** docs/non-executable: syntax/link/consistency checks;
- **T1** local/pure: affected unit tests;
- **T2** contract/persistence-adjacent: unit + contract + selected integration;
- **T3** security/tenancy/migration/distributed side effects: add permanent negative/failure/security suites;
- **T4** release/runtime/database/infrastructure: broad regression + operational evidence.

Run cheap checks first. Release pipelines own the full release safety suite.

# 10. Test Impact Analysis

Prefer dependency-aware affected tests. The selector must be explainable and conservatively fall back broader when uncertain. Security/tenant release gates are never skipped by local impact optimization.

# 11. Flaky Tests

A flaky test is a defect. Never rerun until green. Temporary quarantine is visible, tracked, reasoned and has removal conditions. Avoid arbitrary sleeps, order dependencies and uncontrolled network reliance.

# 12. Contract-Derived Cases

Applicable contract tests cover:

- happy path;
- boundary/invalid input;
- unauthenticated/unauthorized;
- wrong tenant;
- concurrency conflict;
- retry/idempotency duplicate;
- dependency failure/degradation;
- protected-state violation.

Do not multiply combinatorial cases without distinct risk.

# 13. Development Tool Security

Tools able to mutate arbitrary data, impersonate, bypass masks or simulate privilege receive security review. Test production **policy** against synthetic data rather than requiring production data. Shared development environments use stricter controls than a single developer workstation. Local dev services bind safely by default.

# 14. Delivery Obligation Verification

Every concrete application must provide evidence for applicable backup/restore, health/readiness, abuse/rate policy, lifecycle, resilience and deployment obligations in Document 05. Mechanism existence alone is not proof.

# 15. Toolbox Verification

Mature toolbox entries should have stable contract tests/examples sufficient for future agents to consume them without implementation inspection. If a test reveals the toolbox lacks a reusable primitive, do not immediately code it: raise the Toolbox Gap Decision and await user choice.

# 16. Reproducible Failure Bundle

Record, where applicable: build/commit, scenario, seed, tenant/test identity, steps, expected/actual, correlation ID and relevant logs. Handovers include tests/evidence already run.

# 17. Cost Controls

Fast inner loop and strong outer loop are complementary. Track expensive test runtime/compute/external API/AI cost where useful. Prune redundant tests and stale fixtures while preserving invariant coverage.

# 18. Development Model DoD

Complete when the implementation demonstrates trusted environment identity, safe dev-only gating, deterministic baseline/scenarios, populate/append/reset/clear, fakes, controllable time/random, protected state, production-safe defaults, masking policy, contract-derived tests, affected-test selection with safe fallback, flaky policy and reproducible failure evidence.

# 19. Repair, Replay and Debugging

Use this recovery hierarchy: normal application/API -> approved admin/Data Inspector -> controlled repair command/script -> direct database operation only when explicitly authorized. Repair tools support dry-run where practical, validate target environment/tenant and preserve audit/protected invariants.

Provide safe inspection/replay for failed jobs/events/DLQ when the selected queue model supports it. Replay preserves idempotency and trusted context; it is not “run arbitrary payload as system”. Production debugging does not normalize direct mutation or production credentials on developer machines.

# 20. Test Isolation and Parallelism

Tests do not depend on execution order. Parallel tests use isolated tenant/database/schema/resources as appropriate. Referential integrity remains valid during reset. Shared test/staging environments have cleanup/ownership policy; staging is not an uncontrolled playground.

# 21. Specialized Verification — Use Only When It Adds Risk Coverage

Property-based, fuzz, mutation, snapshot/golden and performance/load testing are tools, not mandatory ceremony. Use them when they expose meaningful classes of failure better than ordinary tests. Snapshot/golden files are reviewed as behaviour, not blindly updated. Large test profiles have explicit purpose and cost budget.

# 22. Canonical Scenarios

Maintain concise named scenarios sufficient to prove recurring invariants, including as applicable:

- minimum operable/recovery state;
- no-domain Blank state;
- multi-tenant cross-tenant denial;
- administrative recovery;
- session/time expiry via fake clock;
- key/credential rotation;
- provider/queue failure and replay;
- migration upgrade;
- Unicode/locale/timezone boundaries;
- exact money/currency behaviour;
- idempotency duplicate;
- concurrency/protected-state conflict.

# 23. Verification Governance

Tests have ownership and descriptive behaviour names. Always-run suites are limited to cheap, critical checks; broader release suites run at appropriate gates. Test-selection logic/dependency graph is itself tested where relied upon. Unchanged code may still need tests when its dependency changed.

CI verifies production policy rejects development-only capabilities and, where build-time exclusion is used, proves dangerous modules are absent/inaccessible. Multiple independent guards protect against accidental production database/reset targeting.

# 24. Developer Commands and Discoverability

A single documented task runner/CLI should expose stable equivalents of setup/start/stop/migrate/reset/seed/scenario/test affected/test full/lint/typecheck/build and relevant job/mail inspection. Exact commands are project-specific and generated into `PROJECT_DEVELOPMENT_COMMANDS.md`. Transient manually-mutated test state is never source of truth.

## Superpowers compatibility

**IF Superpowers is being used:** use applicable Superpowers skills as the execution method, subject to Blank authority, risk, cost, toolbox, contract, security and verification rules.

**ELSE:** use the native Blank workflow in `08_AI_ENGINEERING_OPERATING_MODEL.md`.

Superpowers is optional. No Blank requirement disappears when it is absent, and no Superpowers workflow may override a higher Blank authority.
