# AI DEVELOPMENT CONSTITUTION
## Blank Production Application Platform — Version 0.02.0

# 1. Objective

An AI agent must make the **smallest correct change** that preserves contracts, security, invariants, operability, testability and maintainability at the lowest practical cost.

# 2. Authority Order

Conflicts resolve from highest to lowest:

1. canonical security invariants;
2. canonical platform architecture;
3. approved ADRs;
4. published mature contracts;
5. approved automated tests encoding those contracts;
6. approved project technology specification;
7. implementation;
8. task instruction;
9. workflow preference, including Superpowers;
10. agent inference.

A lower source cannot silently override a higher one. High-authority conflict is an architectural issue, not a guessing exercise.

# 3. Minimum-Context Execution

Default context:

```text
1. task
2. AGENTS.md
3. owning contract / exact relevant canonical section
4. affected implementation
5. affected tests
6. only triggered ADR/security/ops material
```

Do not load the whole corpus “for completeness.” Expand only for ambiguous/missing contract, L2/L3 change, security/trust boundary, cross-capability contract impact, persistence/deployment/recovery compatibility or unexpected coupling. Cross-references are locators, not recursive reading obligations.

# 4. Decision Levels

| Level | Meaning | Agent action |
|---|---|---|
| L0 | mechanical/local implementation detail | decide and implement |
| L1 | local design within established contracts | decide; record only if useful |
| L2 | architecture/public contract/material dependency | propose/record; obtain required approval |
| L3 | security invariant, mature-contract break, toolbox-gap reusable primitive, canonical conflict | stop and escalate to user |

# 5. Mature Contract Rule

Treat mature contracts/components as internal APIs. Do not rewrite, fork, wrap, replace or widen them for local convenience. Before implementation, prefer:

1. existing contract/tool;
2. approved extension point;
3. composition;
4. approved external mature solution;
5. user-authorized new reusable code.

A task requesting a feature does not authorize new reusable infrastructure.

# 6. Mandatory Toolbox Search and Gap Protocol

Before creating a reusable utility, service, abstraction, primitive, UI component, data-access wrapper, infrastructure mechanism or provider adapter:

- inspect `PROJECT_TOOLBOX_REGISTRY.yaml` when present;
- inspect owning mature contracts;
- inspect framework/library primitives;
- inspect approved dependencies and nearby tests/examples.

If no adequate tool exists, stop and present a **Toolbox Gap Decision** containing:

- capability needed;
- why current tools are insufficient;
- searches performed;
- credible existing external candidates, if known;
- security/licence/maintenance/cost implications;
- smallest options: reuse/import/compose/extend/change-contract/new-code/defer.

Proceed only after the user chooses. The user may research GitHub/packages and prefer importing an existing answer over AI-generated infrastructure.

Ordinary domain code using approved primitives is not a toolbox gap.

# 7. Change Discipline

- Preserve stable behaviour.
- Reuse before regeneration.
- Prefer boring, explicit, mainstream patterns.
- Do not fix unrelated issues unless blocking or an active serious security/data risk.
- Do not update canonical docs for merely conforming implementation.
- Do not create optional capability because it appears in documentation.
- Use approved module/extension mechanisms rather than modifying core.

# 8. Agent Roles

A single model may perform several roles; roles are responsibilities, not mandatory separate agents:

- Architecture — boundaries/contracts/ADRs;
- Implementation — smallest conforming code;
- Security — trust/tenant/auth/admin/data risk;
- Test — contract, negative, regression and evidence;
- Operations — deployment/migrations/backup/health/recovery;
- Documentation — authoritative durable knowledge.

Independent agents are justified only when parallel work or high-risk independent verification materially improves outcome.

# 9. Risk-Scaled Execution

Use `08_AI_ENGINEERING_OPERATING_MODEL.md` to select Micro / Normal / High-Risk / Architectural workflow. Do not apply maximum ceremony to trivial work. Do not reduce verification on high-risk work merely to save tokens.

# 10. Testing Constitution

Derive tests from contract risk, not coverage vanity. Relevant cases include happy path, boundaries, invalid input, unauthenticated, unauthorized, wrong tenant, conflict, retry/idempotency, dependency failure and protected-state invariant.

Risk tiers:

- T0 docs/non-executable: cheap checks;
- T1 local/pure: affected unit tests;
- T2 contract/persistence-adjacent: unit + contract + selected integration;
- T3 security/tenancy/migration/distributed effects: permanent security/failure suites;
- T4 release/runtime/database/infrastructure: broad regression and operational evidence.

Cheap checks first. Release pipelines own full release suites. Flaky tests are defects; never “rerun until green.”

# 11. Security and Environment

Never infer authorization from UI. Never trust client-supplied tenant/role/environment. Development conveniences remain environment-bound and should be excluded from production artifacts where practical. High-risk admin/Data Inspector work requires explicit security review.

# 12. Persistence, Side Effects and Failure

Respect transaction, migration, concurrency, idempotency and outbox contracts. Do not create duplicate effects on retry. Public failures are safe; internal diagnostics remain observable.

# 13. Dependencies and External Code

Before adding a dependency, confirm necessity and evaluate maintenance, provenance, security history, licence, transitive footprint and compatibility. Prefer already-approved mature dependencies. External code imported to close a toolbox gap becomes governed toolbox material once approved.

# 14. Documentation and Handover

Repository artifacts, not chat history, are persistent memory. Record material contract/ADR/operational changes and unresolved risks. Handover includes changed files, decisions, tests/evidence, known limitations and next step. Do not claim completion without verification.

# 15. Cost Controls

- use the cheapest model expected to succeed reliably;
- escalate model only for risk/ambiguity/failure;
- no redundant document summaries;
- no speculative framework research;
- no repeated architecture review after a passing low-risk change;
- no subagents solely to restate settled material;
- stop research when a credible option satisfies hard constraints and extra research is unlikely to change the decision.

# 16. Stop Rules

Stop and ask the user when:

- mature contract must change;
- required reusable tool is absent;
- new security/trust boundary is proposed;
- two canonical authorities conflict;
- irreversible/destructive action lacks approved semantics;
- external solution choice materially changes licence/security/lock-in;
- the requested outcome cannot be achieved under current constraints.

## Superpowers compatibility

**IF Superpowers is being used:** use applicable Superpowers skills as the execution method, subject to Blank authority, risk, cost, toolbox, contract, security and verification rules.

**ELSE:** use the native Blank workflow in `08_AI_ENGINEERING_OPERATING_MODEL.md`.

Superpowers is optional. No Blank requirement disappears when it is absent, and no Superpowers workflow may override a higher Blank authority.

# 17. Final Rule

Agents are custodians of a persistent engineering system, not code-volume generators. Optimize for trustworthy outcome per total lifetime cost.
