# TECHNOLOGY IMPLEMENTATION RECIPE
## Companion to Document 06 — Version 0.02.0

# 1. Purpose

Turn technology-independent Blank into a concrete, still-domain-empty platform. Document 06 records **what was chosen**; this recipe tells the team **how to reach those choices and outputs**.

# 2. States

```text
A. Canonical Blank (technology-independent)
        ↓
B. Concrete Blank Platform (specific stack, still no domain)
        ↓
C. Domain Application
```

This recipe governs A -> B.

# 3. Start With Constraints, Not Products

Record deployment owner, hosting/residency, realistic scale, availability/recovery expectation, budget, operating skill, browser/client scope, self-hosting/commercial/licence constraints, portability/lock-in tolerance and AI-cost priority. Unknowns may be assumptions; do not fabricate precision.

# 4. Use Decision Waves

1. constraints;
2. foundation stack;
3. security/identity/tenancy;
4. persistence/audit/events;
5. async/files/providers;
6. operations/deployment;
7. dev/test/toolbox;
8. optional capabilities;
9. concrete scaffold and derived agent artifacts;
10. domain-entry acceptance.

Do not process the entire Document 06 in one AI context. Load only current-wave contracts/security sections.

# 5. Foundation Stack Rule

Choose the smallest mature stack satisfying hard contracts. Normally compare 2–4 credible options, reject hard failures, choose, record material ADR, stop researching. Prefer one language/runtime/framework family and modular monolith before service split.

# 6. Persistence / Validation / Secrets Are Foundational

Concrete choices must explicitly establish:

- persistence/data-access semantics and selected mature data layer;
- trusted-boundary validation mechanism;
- secret/key storage/injection.

Do **not** build wrapper CRUD APIs simply because Blank has a persistence contract. Reuse mature ORM/database primitives and standardize only the semantics Blank owns.

# 7. Security Wave

Resolve identity source, session revocation, trusted tenant context, centralized default-deny authorization, elevation/admin/Data Inspector controls, secrets/keys, TLS/proxy trust and app security/abuse controls. Load only relevant portions of Documents 03/04.

# 8. Persistence / Consistency Wave

Resolve database/ORM, tenant scoping/RLS, transactions, concurrency, migrations, outbox/events, idempotency, audit and backup mechanism. Production rollback is not assumed to reverse data migrations safely.

# 9. Async / Files / Provider Wave

Resolve queue/worker/scheduler only as required. Providers sit behind existing platform contracts. Uploaded files use private object storage, authorization and required scanning. Do not add services merely because they are common architecture diagrams.

# 10. Operations / Delivery Obligations

Before production, explicitly address:

- backup/restore/DR evidence;
- health/readiness/graceful startup/shutdown;
- rate-limit/abuse assessment;
- data lifecycle;
- testing/verification;
- dependency resilience;
- environment separation and production admin controls.

A delivery obligation is not automatically a new framework capability. First state how existing platform/toolbox capabilities satisfy it.

# 11. Developer / Test Laboratory

Provide deterministic setup/start/stop/migrate/reset/seed/scenario/test/lint/typecheck/build commands; synthetic scenarios; fake providers; fake clock/random; protected-state invariants; production-policy tests; affected-test selection with safe full-suite fallback.

# 12. Toolbox Construction

As the concrete stack stabilizes, populate `PROJECT_TOOLBOX_REGISTRY.yaml` with mature reusable contracts, selected framework/library primitives and approved external dependencies.

Before writing reusable code:

```text
Toolbox -> contract extension -> composition -> approved dependency/external solution -> USER DECISION -> bespoke reusable code
```

A Toolbox Gap Decision is mandatory before the last step. The user may search GitHub/packages and choose import rather than generation.

# 13. Technical Spikes

Use a narrow spike only where documentation cannot resolve a material uncertainty, e.g. immediate session revocation, ORM/RLS transaction context, rolling migration, queue/outbox semantics or Data Inspector introspection. Record result; discard spike code unless explicitly promoted.

# 14. Scaffold Only After Foundation Choices

Recommended order:

```text
repo/build/CI
environment/config/secrets
database/migrations
identity/auth/sessions
tenancy/organisation/authorization
audit/API/errors/validation
outbox/jobs/idempotency
flags/config/notifications/files
privacy/maintenance/observability
platform admin/Data Inspector
test-data laboratory
backup/restore acceptance
```

# 15. Derived Project Artifacts

Regenerate after scaffold/technology changes:

- `PROJECT_AGENTS.md`;
- `PROJECT_AGENT_CONTEXT_MAP.yaml`;
- `PROJECT_TECHNOLOGY_PROFILE.yaml`;
- `PROJECT_PLATFORM_CAPABILITY_REGISTRY.yaml`;
- `PROJECT_TOOLBOX_REGISTRY.yaml`;
- `PROJECT_TOOLBOX_POLICY.md`;
- `PROJECT_DEVELOPMENT_COMMANDS.md`;
- `PROJECT_ENVIRONMENT_MATRIX.yaml`;
- `PROJECT_DELIVERY_OBLIGATIONS.md`;
- project cost/practicality review.

Do not regenerate canonical 00–08 merely because technology was selected.

# 16. Domain-Entry Gate

Before real domain work prove: build/start, fresh migration, secure bootstrap, auth/revocation, tenant creation/cross-tenant denial, default-deny authz, audit/config/job, health/logging, deterministic test data/protected state, admin/Data Inspector restrictions, backup mechanism, current agent/toolbox artifacts. Use one disposable trivial module to prove extension, then remove/retain only as test example.

# 17. Cost Rules

- reuse prior approved decisions;
- batch related decisions;
- compare only credible candidates;
- use targeted canonical context;
- create ADRs only for material choices;
- do not repeatedly reopen approved technology without trigger;
- do not spawn agents to restate documentation;
- do not implement optional enterprise services before need.

Reconsider on vulnerability/EOL, measured performance/cost failure, inability to meet contract, operational burden, licence/vendor degradation or new hard requirement. Preference alone is insufficient.

## Superpowers compatibility

**IF Superpowers is being used:** use applicable Superpowers skills as the execution method, subject to Blank authority, risk, cost, toolbox, contract, security and verification rules.

**ELSE:** use the native Blank workflow in `08_AI_ENGINEERING_OPERATING_MODEL.md`.

Superpowers is optional. No Blank requirement disappears when it is absent, and no Superpowers workflow may override a higher Blank authority.

# 18. Final Rule

Make the minimum deliberate technology decisions needed for a trustworthy concrete Blank Platform, then give agents small exact facts, paths, commands and toolbox entries.
