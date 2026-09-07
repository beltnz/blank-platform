# AGENTS.md — Blank Platform 0.02.0

Start here. Do **not** preload the canonical corpus.

## Authority

Security invariants -> architecture -> ADRs -> mature contracts -> tests -> project technology -> implementation -> task -> workflow preference.

## Default context

Task + this file + owning contract + affected code/tests + only triggered security/ADR/ops sections. Use `AGENT_CONTEXT_MAP.yaml` to route.

## Reuse / Toolbox Rule

Before creating reusable code, search `PROJECT_TOOLBOX_REGISTRY.yaml` (when present), mature contracts, extension points, selected framework/library primitives and approved dependencies.

**If adequate tool exists:** use it.

**If it does not:** STOP and raise a Toolbox Gap Decision to the user. A feature request does not authorize new reusable infrastructure. The user may prefer an existing GitHub/package solution. Mature contracts are immutable by default.

## Superpowers

IF Superpowers is being used, use applicable skills under `08_AI_ENGINEERING_OPERATING_MODEL.md`. ELSE use the native Blank workflow there. Blank authority/risk/cost/toolbox/security rules always win.

## Change order

Existing contract/tool -> extension point -> composition -> approved external mature tool -> user-authorized new reusable code. Keep changes local; no unrelated cleanup.

## Risk

L0/L1 routine work: minimal process. L2 architecture: propose/record/approve. L3 security invariant, mature-contract change or toolbox gap: stop for user decision.

Verification: T0 cheap docs checks; T1 affected unit; T2 contract/integration; T3 security/tenancy/migration/failure suites; T4 release/ops evidence. Never rerun flaky tests until green.

## Non-negotiables

Default deny; server-side tenant isolation; UI not security; secrets absent from source/logs; no custom crypto/auth protocol; no float money; retries controlled/idempotent; audit not ordinarily mutable; production admin/Data Inspector stricter than development; development powers do not silently ship to production.

## Canonical locators

- `01_CANONICAL_PLATFORM_ARCHITECTURE.md` — boundaries/invariants/taxonomy
- `02_AI_DEVELOPMENT_CONSTITUTION.md` — agent governance
- `03_PLATFORM_CAPABILITY_CONTRACTS.md` — reusable contracts
- `04_PLATFORM_SECURITY_MODEL.md` — security
- `05_BLANK_PLATFORM_DEFINITION_OF_DONE.md` — acceptance/delivery obligations
- `06_TECHNOLOGY_IMPLEMENTATION_SPECIFICATION_TEMPLATE.md` — concrete stack
- `06A_TECHNOLOGY_IMPLEMENTATION_RECIPE.md` — A->B procedure
- `07_DEVELOPMENT_TEST_DATA_AND_VERIFICATION_MODEL.md` — dev/test
- `08_AI_ENGINEERING_OPERATING_MODEL.md` — workflow/model/cost/Superpowers

If the owning contract is clear and no L2/L3 trigger exists, do the work without broadening context.
