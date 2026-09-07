# CANONICAL PLATFORM ARCHITECTURE
## Blank Production Application Platform — Version 0.02.0

# 1. Architectural Objective

Blank is a reusable, technology-independent production foundation. It must be deployable and operable without containing business-domain semantics.

Canonical dependency direction:

```text
Domain -> Platform Contracts -> Platform Implementations -> Infrastructure
```

No lower layer may import or encode business concepts from a higher layer.

# 2. Requirement Taxonomy

Use these classifications consistently:

| Type | Question | Examples |
|---|---|---|
| Foundation Capability | What reusable interface can code consume? | identity, authorization, validation, persistence semantics, audit, configuration |
| Platform Service | What reusable operational mechanism exists? | jobs, notifications, object storage, feature flags, health |
| Cross-Cutting Policy | What rule applies everywhere? | tenant isolation, safe failure, idempotency, toolbox-first reuse |
| Delivery Obligation | What must this deployment prove? | restore test, RPO/RTO, rate-limit assessment, lifecycle policy, release verification |

A mechanism may also have a delivery obligation. Keep the mechanism and proof distinct.

# 3. Canonical Context and Identity

Operations may carry a trusted execution context containing actor, tenant, organisation, session, locale/timezone and correlation metadata. Untrusted clients may request context; they do not establish trusted context.

Authentication proves identity. Authorization evaluates:

```text
Subject + Action + Resource + Context -> AuthorizationDecision
```

Rules:

- default deny;
- server-side enforcement;
- tenant membership/scope explicit;
- platform administration distinct from tenant administration;
- impersonation preserves true actor and effective actor;
- elevated/break-glass access is temporary, explicit and audited.

# 4. Tenancy and Organisation

Users may belong to multiple tenants. Tenant context must be established from trusted identity/membership state. Tenant isolation uses defense in depth:

```text
identity -> trusted tenant context -> authorization -> query scoping -> database controls/RLS where supported
```

Database RLS may strengthen isolation; it is not the sole boundary. Cross-tenant denial tests are permanent.

# 5. Persistence and Data Access

Persistence is foundational, but Blank must not duplicate adequate database/ORM primitives. The platform standardizes:

- tenant scoping;
- transaction boundaries;
- concurrency/optimistic conflict semantics;
- canonical persistence errors;
- migration ownership/order;
- approved raw-query escape policy;
- observability/audit requirements;
- testability and provider substitution where justified.

Use native temporal/database types. Production schema evolution is forward-oriented: expand -> migrate -> contract. Rollback is not presumed safe.

# 6. Validation and API Boundary

All external input is untrusted. Structural validation occurs at trusted service boundaries before business logic/persistence. Validation does not replace authorization.

APIs define:

- canonical error model;
- bounded pagination/filter/sort;
- request/body limits;
- idempotency for retryable mutations;
- optimistic concurrency where conflicts matter;
- correlation IDs;
- safe public errors;
- version/lifecycle policy.

# 7. Configuration, Secrets and Flags

Configuration is typed and deterministic, with explicit definitions, scopes, precedence, validation and audit. Secrets are separate from configuration and supplied by approved secret-management mechanisms. Feature flags answer **whether** behaviour is enabled; configuration answers **how** it behaves. Flags never replace authorization.

# 8. Audit and Event Publication

Security/significant operations produce append-only audit records. Ordinary application paths cannot mutate audit history. Avoid blanket full-record snapshots when selective metadata/diffs satisfy accountability with less PII. Retention/legal-hold rules remain explicit.

Required durable event publication uses a transactional outbox or equivalent consistency mechanism. Consumers assume duplicate delivery and are idempotent where retry can occur.

# 9. Background Work and External Dependencies

Queued/scheduled work carries trusted tenant/actor/correlation context, bounded retries, timeout, idempotency semantics, dead-letter/recovery behaviour and graceful shutdown. Internal queue origin does not imply trust.

External dependencies define criticality, timeout, retry, degradation, health effect, user-visible effect and observability. Retries use bounded backoff/jitter and must not amplify outages.

# 10. Time, Locale and Money

Distinguish:

- Instant;
- LocalDateTime;
- CalendarDate;
- Duration;
- Timezone.

Persist instants in UTC with explicit timezone interpretation. Use a `Clock` abstraction for deterministic tests.

Money is `{amount, currency}`, exact decimal, ISO 4217, explicit precision/rounding; never binary floating point. Internationalization uses explicit locale/timezone/currency context and UTF-8.

# 11. Notifications and Object Storage

Notifications are reusable platform services; product messaging is domain functionality. Provider SDKs remain behind adapters/contracts.

Object storage supports authorized upload/download, metadata, lifecycle and temporary access. Large files may transfer directly to storage. Validate content/size/type, use safe names, isolate processing, and scan untrusted uploads where required. Object keys are not authorization tokens.

# 12. Privacy and Data Lifecycle

Provide reusable mechanisms where applicable for acceptance/consent, export, deletion/anonymisation, retention and legal hold. Software alone does not guarantee regulatory compliance.

Each application must separately define lifecycle behaviour for its actual data classes, including backup treatment.

# 13. Observability, Health and Maintenance

Standard observability includes structured logs, metrics, correlation, tracing where useful, error tracking, liveness and readiness. Logs exclude secrets and unnecessary PII.

Health/readiness is both a reusable service and a delivery obligation: the deployment must prove signals reflect safe traffic acceptance.

Maintenance/degradation semantics define API/browser behaviour, sessions, jobs, admins, integrations and health. Maintenance is not only a UI switch.

# 14. Platform Administration and Data Inspector

Platform administration is explicitly privileged. High-risk operations use recent/strong authentication, capability-specific permission, short-lived elevation, confirmation/reason where appropriate and full audit.

The Platform Data Inspector may browse schema/data and perform controlled mutation/queries.

- ordinary users: none;
- tenant admins: no DB-level access by default;
- development: convenient within environment policy;
- production: materially stronger controls;
- direct SQL: production-disabled by default unless explicitly approved.

Inspector operations do not bypass tenant, authorization, audit or environment policies.

# 15. Development/Test Laboratory

Trusted environment identity comes from deployment configuration, never client input. Development/test may provide synthetic data, reset/seed/scenarios, fake providers, controllable clock/random, failure injection and job replay. Production defaults deny/omit dangerous development powers.

Protected state is enforced by invariant, not magic immortal records: e.g. preserve at least one viable recovery administrator and required active keys/migration history.

# 16. Security, Supply Chain and Recovery

Use standard cryptography and mature security libraries; never invent primitives/protocols. Evaluate dependencies for maintenance, provenance, vulnerabilities, licence and transitive footprint. Lockfiles/reproducible resolution are required where supported.

Backups, restore and DR are primarily delivery obligations supported by platform/infrastructure mechanisms. Production must define backup, retention, restore procedure, restore testing, RPO/RTO and independently recoverable critical credentials.

# 17. Extensibility

Domain modules may add entities, migrations, routes, permissions, navigation, config, flags, jobs, audit events, notifications and UI through approved extension points. Adding a domain module should be additive, not invasive.

# 18. Mature Contract and Toolbox Invariant

Mature contracts are immutable by default. Before creating any reusable primitive, wrapper, helper, UI primitive, database abstraction or infrastructure mechanism:

1. search the project toolbox/registry;
2. search existing contracts/extension points;
3. search selected framework/library primitives and approved dependencies;
4. if still missing, **stop and ask the user**.

The user decides whether to import an existing external solution, compose/extend current tools, alter a mature contract, authorize bespoke code, or change/defer the requirement.

# 19. Delivery Obligations

Every concrete application must explicitly address, with evidence or recorded `NOT APPLICABLE` rationale:

- backup/restore/DR;
- health/readiness/graceful startup/shutdown;
- rate limiting/abuse protection;
- data lifecycle;
- testing/verification;
- operational resilience;
- environment separation;
- secret/key handling;
- production admin/Data Inspector controls;
- deploy/recovery procedure.

A toolbox gap discovered while meeting an obligation follows the same mandatory human-review rule.

# 20. Canonical Invariants

1. Authentication and authorization are separate.
2. Authorization defaults to deny.
3. Tenant isolation is server-enforced.
4. UI/client state is never the sole security boundary.
5. Platform code does not depend on domain code.
6. Mature contracts are immutable by default.
7. Missing reusable tooling requires user approval before new reusable code.
8. Existing mature primitives are reused rather than duplicated/wrapped without need.
9. Secrets are absent from source and ordinary logs.
10. Passwords are never reversibly stored.
11. External input is untrusted and validated.
12. Monetary arithmetic never uses binary floating point.
13. Production migrations are not presumed reversible.
14. Retryable effects are idempotent/deduplicated.
15. Ordinary app code cannot mutate audit history.
16. Dangerous admin operations require explicit privilege.
17. Production Data Inspector controls exceed development controls.
18. Public errors do not reveal sensitive internals.
19. Material dependency failure fails safely.
20. Critical boundaries have permanent automated tests.
21. Environment identity is trusted server/deployment state.
22. Development powers do not silently exist in production.
23. Recovery is not complete until restore is proven.
24. Delivery obligations require evidence, not assumption.
25. Optional complexity is not backlog authorization.

## Superpowers compatibility

**IF Superpowers is being used:** use applicable Superpowers skills as the execution method, subject to Blank authority, risk, cost, toolbox, contract, security and verification rules.

**ELSE:** use the native Blank workflow in `08_AI_ENGINEERING_OPERATING_MODEL.md`.

Superpowers is optional. No Blank requirement disappears when it is absent, and no Superpowers workflow may override a higher Blank authority.
