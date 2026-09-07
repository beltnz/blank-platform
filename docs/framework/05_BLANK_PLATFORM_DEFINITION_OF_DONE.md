# BLANK PLATFORM DEFINITION OF DONE
## Acceptance and Release Gate — Version 0.02.0

# 1. Use

This is evidence-based acceptance, not a roadmap. Status values: `PASS`, `FAIL`, `NOT APPLICABLE`, `BLOCKED`.

Severity:

- **GATE-A** — cannot release with failure;
- **GATE-B** — must be resolved or formally accepted before production;
- **GATE-C** — conditional/desirable when applicable.

Valid evidence may be reused until a relevant change invalidates it. Task completion is not platform release.

# 2. Architecture and Blankness

- **A** Build/deploy contains no business-domain semantics.
- **A** Platform->domain dependency is absent and architecture test enforces it.
- **A** Stable public contracts are documented/versioned.
- **A** Domain extension is additive through approved extension points.
- **A** Mature contracts/tools are registered and protected from casual change.

# 3. Toolbox / Reuse Gate

- **A** `PROJECT_TOOLBOX_REGISTRY.yaml` (or equivalent) identifies approved mature reusable tools.
- **A** New reusable primitive has evidence of prior toolbox/contract/framework/dependency search.
- **A** Any unresolved toolbox gap stopped for user decision before bespoke reusable code.
- **A** No unnecessary duplicate UI/data/infrastructure primitive exists.
- **B** Imported external toolbox code has security/licence/maintenance/compatibility review.

# 4. Identity / Authentication / Session

- **A** identity lifecycle works;
- **A** authentication uses approved mature mechanisms;
- **A** session expiry/revocation works;
- **A** privileged elevation/recent auth works where required;
- **A** account recovery does not bypass security;
- **B** federation/linking rules are tested if enabled.

# 5. Tenancy / Authorization

- **A** authorization defaults deny;
- **A** tenant context is trusted server-side state;
- **A** tenant A cannot access tenant B data/actions;
- **A** platform admin != tenant admin;
- **A** UI hiding is not sole enforcement;
- **A** wrong-tenant/privilege-escalation tests are permanent.

# 6. Persistence / Validation / API

- **A** persistence uses canonical tenant/transaction/error/concurrency semantics;
- **A** database integrity constraints exist where material;
- **A** external input is structurally validated;
- **A** canonical safe error model is used;
- **B** pagination/filter/sort/request limits are bounded;
- **B** retryable mutations define idempotency;
- **B** conflict-sensitive mutation defines concurrency behaviour.

# 7. Migration / Event / Jobs

- **A** fresh database migrates from zero;
- **A** production migration path is privileged/locked/traceable;
- **A** destructive migration is reviewed and not assumed reversible;
- **A** required event publication is transactionally reliable;
- **A** jobs preserve tenant/context and do not acquire accidental global privilege;
- **B** retries/DLQ/replay are bounded and idempotent.

# 8. Config / Secrets / Flags / Crypto

- **A** typed configuration and deterministic precedence work;
- **A** production secrets use approved secure mechanism and differ from development;
- **A** secret values are absent from config UI/log/source/generated docs;
- **B** critical secret/key rotation procedure exists;
- **A** no bespoke cryptography;
- **B** feature flags are deterministic/auditable and never authorization.

# 9. Audit / Privacy

- **A** required security/admin actions create audit evidence;
- **A** ordinary paths cannot mutate/delete audit history;
- **B** audit avoids unnecessary PII;
- **B** configured export/deletion/anonymisation works where applicable;
- **B** deletion respects retention/legal hold/audit integrity.

# 10. Files / Notifications / External Providers

- **A** protected object access is authorized and tenant-isolated where storage is enabled;
- **A** untrusted upload limits/type/content checks exist;
- **B** required malware scan gates availability;
- **B** provider adapters isolate application code from vendor SDKs;
- **B** notifications/retries do not create uncontrolled duplicates.

# 11. Observability / Health

- **A** logs are structured and secret-safe;
- **B** request/job correlation works;
- **B** core metrics/errors are observable;
- **A** liveness and readiness exist;
- **A** readiness reflects unsafe dependency state correctly;
- **A** health endpoints leak no sensitive detail.

# 12. Administration / Data Inspector

- **A** platform admin requires explicit authenticated authorization;
- **A** dangerous operations use stronger controls where policy requires;
- **A** Data Inspector unavailable to ordinary users/tenant admins by default;
- **A** production restrictions exceed development;
- **A** direct SQL production-disabled unless explicitly approved;
- **A** inspector mutations/queries are bounded/audited and cannot bypass tenant policy.

# 13. Environment / Development Laboratory

- **A** trusted environment identity exists;
- **A** production data/secrets are separated from development/test;
- **A** test reset/fake/failure-injection powers are denied or absent in production;
- **B** deterministic seed/scenarios/fake clock/providers exist;
- **A** protected system-state invariants prevent loss of minimum recovery operability;
- **B** production-derived test data is masked under explicit policy.

# 14. Delivery Obligations — Mandatory Evidence

These are not automatically foundation capabilities; every concrete application must address them explicitly.

## 14.1 Backup / Restore / DR
- **A** automated production backup mechanism;
- **B** retention documented;
- **A** backup access protected/encrypted;
- **A** successful controlled restore evidence;
- **B** RPO and RTO documented;
- **B** critical recovery credentials independently recoverable.

## 14.2 Health / Graceful Failure
- **A** startup/readiness/shutdown behaviour verified;
- **B** dependency failure/degradation behaviour documented/tested.

## 14.3 Rate Limiting / Abuse
- **A** public/auth/admin/expensive operations assessed;
- **A** applicable limits/abuse controls implemented or `NOT APPLICABLE` with rationale;
- **B** failure policy of rate-limit infrastructure is explicit.

## 14.4 Data Lifecycle
- **B** data classes have retention/deletion/anonymisation/export policy where applicable;
- **B** backup/archive treatment is explicit.

## 14.5 Verification
- **A** required unit/integration/contract/security/architecture tests pass;
- **A** migration verification passes;
- **A** no “rerun until green”;
- **B** test impact selection falls back conservatively when uncertain.

## 14.6 Operational Resilience
- **A** critical dependencies have finite timeout and safe failure;
- **B** retry/idempotency/degradation/circuit-breaking decisions are explicit where relevant.

# 15. Deployment / Operations

- **A** deployment is repeatable and does not rely on undocumented manual steps;
- **A** config/secrets are injected outside source;
- **A** migrations coordinate safely;
- **A** readiness is validated before traffic;
- **B** failed release has documented recovery;
- **B** maintenance/read-only behaviour is known;
- **B** resource/cost guardrails are defined before production where material.

# 16. Supply Chain

- **A** dependency resolution is reproducible where supported;
- **A** known critical vulnerabilities are resolved or explicitly accepted;
- **B** dependency inventory/licence review exists;
- **B** CI secrets/permissions are least-privilege.

# 17. Domain-Entry Gate

Before first real domain module: clean build/start, fresh migration, secure bootstrap, auth/session revocation, tenant creation/cross-tenant denial, default-deny authorization, audit/config/jobs/health/logging, deterministic test data, protected state, admin/Data Inspector restrictions, backup mechanism and current agent/toolbox routing files.

# 18. Release Rule

Production readiness is evidence, not confidence. Each applicable GATE-A must pass. GATE-B must be resolved or explicitly accepted by authorized humans. `NOT APPLICABLE` requires rationale. A missing toolbox capability is never silently satisfied with newly invented reusable code.

# 19. Additional Product and Integrity Gates

- **A Documentation:** canonical docs/ADRs/contracts/runbooks required by the current architecture exist and agree; derived files do not override authority.
- **A Build/start:** clean checkout installs/builds/starts through documented commands; fresh installation is reproducible.
- **A Bootstrap admin:** initial privileged access is secure, non-default and recoverable without an unsafe permanent credential.
- **B Organisation hierarchy:** configured hierarchy/membership scope is enforced where enabled.
- **B Time/i18n/money:** timezone/date boundary cases, Unicode/locale and exact-decimal/currency rules are demonstrated.
- **B Maintenance:** read-only/maintenance/degradation controls behave consistently across API/UI/jobs/health.
- **B Impersonation/break-glass:** if enabled, true actor/effective actor, elevation, expiry, visibility and audit are proven.
- **A Failure modes:** critical dependency failures are observable and do not silently corrupt/security-bypass state.
- **B Performance/resources:** realistic initial resource limits and performance assumptions exist; do not claim untested “internet scale”.
- **B Usability:** core admin/user workflows can be completed without hidden tribal steps; errors are actionable and safe.
- **B Accessibility:** applicable user/admin UI meets the selected accessibility baseline.
- **A Data integrity:** constraints/transactions/concurrency protect material invariants under concurrent failure paths.
- **A Privacy leakage:** logs/errors/exports/cache/search/test artifacts do not expose protected data outside policy.
- **A Release artifact:** build/version provenance and required configuration are identifiable; production artifact excludes dangerous dev-only code where practical.

# 20. Acceptance Drills

Before claiming the applicable maturity level, demonstrate as relevant:

- fresh install from empty state;
- blankness (no hidden domain semantics);
- add/remove disposable extension module without invasive core change;
- protected mature component remains consumable without internal inspection;
- cross-tenant/authorization denial;
- restore from backup;
- production Data Inspector restrictions;
- provider/dependency failure and incident containment;
- migration upgrade path;
- recovery/admin access after simulated failure.

# 21. Evidence, Debt and Sign-Off

No silent failure and no unverified “works” claim. Accepted technical debt names owner, risk, mitigation and trigger/deadline. Release blockers are visible. Production readiness review identifies sign-off roles appropriate to security, engineering and operations risk; one person may hold multiple roles in a small team, but responsibilities remain explicit.

# 22. Scope-Specific Definitions of Done

- **New capability:** satisfy Document 03 capability DoD plus applicable security/tests.
- **Domain module:** use existing extension/toolbox mechanisms; no foundation duplication; tenant/auth/audit/data rules proven.
- **AI task:** requested change complete, affected verification passes, no unauthorized contract/toolbox expansion, handover is durable.
- **Platform release:** all applicable GATE-A pass and GATE-B are resolved/accepted; release evidence is current.

The **minimum production acceptance set** is the applicable GATE-A set plus explicitly required GATE-B obligations. “Gold standard” evidence may add stronger external pen-test, WORM audit, SBOM/signing, chaos/failover exercises, etc., but these are not automatically mandatory without trigger.

## Superpowers compatibility

**IF Superpowers is being used:** use applicable Superpowers skills as the execution method, subject to Blank authority, risk, cost, toolbox, contract, security and verification rules.

**ELSE:** use the native Blank workflow in `08_AI_ENGINEERING_OPERATING_MODEL.md`.

Superpowers is optional. No Blank requirement disappears when it is absent, and no Superpowers workflow may override a higher Blank authority.
