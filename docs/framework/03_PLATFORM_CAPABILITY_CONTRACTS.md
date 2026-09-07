# PLATFORM CAPABILITY CONTRACTS
## Blank Production Application Platform — Version 0.02.0

# 1. Purpose and Scope

This document defines reusable **foundation capabilities and platform services**. Cross-cutting policies live primarily in Documents 01/02/04; delivery evidence lives primarily in Document 05. Do not turn every good engineering practice into a capability.

A contract specifies purpose, responsibilities/non-responsibilities, inputs/outputs/errors, security/tenant semantics, persistence/transaction/idempotency, audit/observability, failure, extension points, dependencies, tests, versioning and invariants as applicable.

Mature contracts are immutable by default. A contract gap is a design/toolbox issue, not permission to invent a parallel abstraction.

# 2. Shared Models

Conceptual `ExecutionContext` may contain Actor, TenantContext, OrganizationContext, SessionContext, CorrelationId, Locale/Timezone and trusted request metadata.

Authorization contract:

```text
Subject + Action + Resource + Context -> AuthorizationDecision
```

Canonical errors include Validation, Authentication, Authorization, NotFound, Conflict/Concurrency, RateLimit, Idempotency, DependencyUnavailable, Configuration and Internal errors. Public representations expose stable safe codes/messages/correlation only.

# 3. Foundation Capability: Identity

Provides stable internal user identity independent of external identity provider. Supports provider links and lifecycle status. Does not itself authorize actions. External identifiers are not trusted tenant/role claims.

# 4. Foundation Capability: Authentication

Establishes identity using mature provider/library mechanisms. Supports required factors/recovery/federation according to technology profile. No custom cryptographic/auth protocol. Authentication result does not grant application permission.

# 5. Foundation Capability: Session Management

Creates, validates, rotates, expires and revokes sessions. Privilege/elevation is explicit and temporary. Stolen/revoked sessions must be terminable according to approved policy. Cookies/tokens follow security model.

# 6. Foundation Capability: Tenancy and Organisation

Defines tenant membership, active trusted tenant context and optional organisation hierarchy. Multi-tenant users are supported. Tenant context comes from trusted membership/session state. Cross-tenant access is denied by default.

# 7. Foundation Capability: Authorization

Central policy boundary implementing default deny. Supports permissions/roles plus contextual predicates. UI visibility may consult authorization but cannot replace it. Platform/tenant admin scopes are distinct.

# 8. Foundation Capability: Persistence / Data Access

Standardizes persistence semantics without duplicating adequate ORM/database primitives. Contract covers:

- tenant scoping;
- transactions;
- concurrency/conflict;
- canonical errors;
- query safety/parameterization;
- raw-query exception policy;
- observability;
- testability.

Domain repositories may exist where they add domain meaning; ceremonial wrappers around mature library CRUD are prohibited.

# 9. Foundation Capability: Validation

Validates type, shape, size, allowed values and cross-field rules at trusted service boundaries. Invalid input is rejected with structured safe errors. Validation never replaces authorization or domain invariants.

# 10. Foundation Capability: Schema Migration

Registers/orders/applies owned migrations with lock/traceability. Production migrations are privileged and forward-oriented. Modules do not silently alter another module's schema. Migration history is protected state.

# 11. Foundation Capability: Configuration

Typed `SettingDefinition` and scoped `SettingValue`, deterministic precedence, validation, audit and environment awareness. Secrets are references/metadata only, not secret values.

# 12. Foundation Capability: Audit

Append-only accountability events for security/administrative/material actions. Records identify actor/effective actor, tenant/context, action, target, result and selected metadata without unnecessary PII. Ordinary app roles cannot update/delete audit history.

# 13. Foundation Capability: API and Error Model

Provides canonical route participation in authentication, trusted tenant context, authorization, validation, correlation, errors and observability. Defines bounded pagination/filter/sort, request limits, versioning, idempotency/concurrency semantics and safe errors.

# 14. Foundation Capability: Idempotency / Concurrency

Retryable mutation defines idempotency key scope/storage/result semantics. Keys are bounded and cannot leak another actor/tenant result. Conflict-sensitive records use version/transaction/constraint/locking semantics as appropriate.

# 15. Foundation Capability: Time / Locale / Money

Provides `Clock` and explicit time value categories; IANA timezone semantics; locale context; exact decimal money with ISO 4217 and explicit rounding/precision.

# 16. Platform Service: Background Jobs

Registers durable jobs with type/version, trusted context, timeout, retry, idempotency, cancellation where practical, status, DLQ/replay and graceful shutdown. A job does not gain system privilege merely because it runs asynchronously.

# 17. Platform Service: Transactional Event Publication

Outbox/equivalent ensures required events are persisted consistently with state change. Event envelope includes type/version, tenant, causation/actor and correlation. Consumers validate and assume at-least-once delivery.

# 18. Platform Service: Notifications

Sends templated system notifications through provider adapters. Supports channel, locale, recipient policy, retry/deduplication and observability. User-to-user messaging is domain/optional functionality.

# 19. Platform Service: Object / Asset Storage

Authorized upload/download/delete/metadata/lifecycle, short-lived access URLs, tenant scope and provider abstraction. Validates size/content/type, isolates processing, supports malware scan where required. Object knowledge is not authorization.

# 20. Platform Service: Feature Flags

Deterministic flag evaluation by environment/tenant/role/percentage where required; audited administration; kill switches fail safely. Flags do not grant authorization.

# 21. Platform Service: Privacy / Data Lifecycle

Reusable mechanisms for policy acceptance/consent, export, deletion/anonymisation, retention classification and legal hold where applicable. The concrete application remains responsible for defining its actual data-class policies.

# 22. Platform Service: Health / Readiness

Provides liveness/readiness and dependency registry. Liveness asks whether restart may help; readiness asks whether traffic/work can be accepted safely. Optional degraded dependencies need not fail readiness if safe degradation is explicit. Endpoints reveal no sensitive internals.

# 23. Platform Service: Maintenance / Degradation

Provides global/scoped maintenance/read-only state, operator messaging and graceful behaviour. Enforcement is server-side. Semantics cover browser/API, jobs, sessions, admins, integrations and health.

# 24. Platform Service: Platform Administration

Privileged administration for identity/tenancy/roles/config/flags/sessions/audit/jobs/health/maintenance/storage/security. Each operation requires server-side explicit permission; dangerous operations may require elevation/reason/confirmation.

# 25. Platform Service: Data Inspector

Provides authorized schema/record inspection, controlled create/edit/delete, migration diagnostics and optional controlled query execution. Strong environment-specific controls; direct SQL is production-disabled by default. Inspector cannot bypass security/audit/tenant policy.

# 26. Foundation Capability: Secrets and Key Access

Provides controlled references/access to secrets and cryptographic keys through approved stores. Supports least privilege, rotation/revocation and audit as provider permits. Secret values never enter ordinary config APIs, source or logs.

# 27. Platform Service: Correlation / Observability Context

Generates/validates bounded correlation IDs and propagates through request, job, external call, log, trace and audit. IDs contain no sensitive data.

# 28. Platform Service: Import / Export / Webhooks / Service Accounts

These standard services are enabled only when required. All participate in canonical authentication/authorization/tenant/validation/audit/idempotency/observability. Webhooks use signing/replay protection; imports validate untrusted data; exports are authorized and protected; service accounts have explicit narrow scope.

# 29. Extension Registration Contracts

Domain modules may register, through approved mechanisms:

- API/UI routes;
- permissions/roles;
- migrations;
- jobs;
- audit event types;
- notification templates;
- navigation;
- settings/flags;
- health dependencies;
- events.

Registration must not bypass canonical middleware/security.

# 30. Capability Registry

The concrete project maintains `PROJECT_PLATFORM_CAPABILITY_REGISTRY.yaml` with capability classification, contract version, implementation/test locations, maturity and dependencies. Mature entries belong in `PROJECT_TOOLBOX_REGISTRY.yaml` where reusable by agents.

# 31. Optional Capabilities

Not mandatory unless promoted by ADR/hard requirement: distributed cache, dedicated search, read replicas, analytics/BI, issue/feedback system, user-to-user messaging, distributed locks, CQRS/read model, service mesh, multi-region active/active. Documentation is not backlog authorization.

# 32. Capability Definition of Done

A capability is complete only when applicable items are explicit and evidenced:

- contract purpose/input/output/error/side effects;
- authorization/tenant/sensitive-data/failure semantics;
- persistence/transaction/concurrency/migration;
- retry/idempotency/degradation;
- audit/log/metric/health;
- contract/negative/cross-tenant/failure tests;
- extension/version documentation.

# 33. Toolbox and Mature Contract Rule

Before adding or changing reusable behaviour:

```text
existing mature tool -> extension point -> composition -> approved external tool -> user-authorized new code
```

If the chain fails, stop and raise a Toolbox Gap Decision. Do not create a parallel interface because the existing one is slightly inconvenient.

# 34. Consolidated Supporting Contracts

The following remain governed contracts/policies even when they do not justify a large standalone subsystem:

- **Application security / rate limiting** — standard enforcement hooks, endpoint-aware policy and explicit fail-open/fail-closed behaviour; delivery-specific limits remain an obligation.
- **Impersonation / elevation** — true actor + effective actor, explicit permission, time-bounded elevation, audit and visible operator state.
- **Permission registry / role management** — stable permission identifiers; roles are managed bundles, not magic hard-coded checks.
- **User preferences / UI theme** — tenant/user-scoped presentation preferences only; never security state. Theme/design tokens use the approved UI toolbox rather than parallel primitives.
- **Terms / policy acceptance** — versioned document identifier, acceptance timestamp/actor/context; distinct from broad regulatory claims.
- **Export / import** — authorized scope, async where large, safe temporary download, schema/version validation, untrusted import handling and audit.
- **Outbound / inbound webhooks** — endpoint ownership, signing/authentication, secret rotation, replay protection, bounded retries, idempotency and delivery inspection.
- **Scheduled tasks** — explicit schedule/timezone, duplicate control, missed-run policy and trusted execution context.
- **Data classification / PII masking** — classification drives handling/display/export/log rules; masking is authorization/context-aware and not data deletion.
- **Soft/hard delete / anonymisation** — explicit semantics; hard delete respects retention/legal hold and referential integrity.
- **Service accounts / API consumers** — non-human principal identity, narrow credentials/scopes, rotation/revocation and tenant boundaries.
- **CORS / CSRF / request-size / pagination / filtering / sorting / bulk operations** — canonical API policy with allowlists/bounds; bulk operations preserve per-item authorization/tenant/invariant semantics.
- **Configuration propagation / runtime kill switch** — deterministic propagation expectations and safe operational disable behaviour.
- **Graceful shutdown** — stop accepting work, drain/finish/cancel safely, close resources and preserve durable work.
- **Read replicas** — optional read-only path; consistency/staleness and tenant/security semantics explicit.
- **Search / cache / distributed locking** — optional abstractions only when a demonstrated need exists; never silently become authorization or source of truth.
- **Analytics/reporting** — optional; query/read models cannot bypass tenant/security boundaries.
- **Issue/feedback** — domain/optional; not mandatory Blank core.
- **Provider adapters** — email, SMS, push, object store, federation, clock, identifier generation and similar providers are replaceable only where substitution has real value; do not wrap merely for ceremony.
- **Identifier / slug generation** — collision/entropy/security expectations explicit; identifiers do not grant authorization.
- **Environment identity / policy** — trusted runtime source with security-sensitive feature gating.
- **Build/version metadata** — operator-visible artifact identity sufficient for diagnostics; public disclosure may be reduced.
- **Operational banner / service degradation** — informational banner does not itself enforce restrictions; dependencies declare criticality, timeout, retry, fallback and health impact.
- **Protected system-state invariants** — minimum operable/recovery state is enforced by rule, not special undeletable record IDs.
- **Test data / scenario / provider substitution / impact analysis** — governed by Document 07 but exposed through stable developer-facing contracts/commands when reusable.

# 35. Contract Lifecycle

- Contract versioning is explicit when consumers can be affected.
- Breaking mature-contract change is L2/L3, requires user approval and migration/deprecation plan.
- Ownership is assigned to a durable team/role.
- Security boundaries and dependencies are documented.
- Consumers read the contract/tests/examples first; implementation internals only when necessary.
- Once a contract becomes mature, register it in the project toolbox so future agents can reuse it without rediscovery.

## Superpowers compatibility

**IF Superpowers is being used:** use applicable Superpowers skills as the execution method, subject to Blank authority, risk, cost, toolbox, contract, security and verification rules.

**ELSE:** use the native Blank workflow in `08_AI_ENGINEERING_OPERATING_MODEL.md`.

Superpowers is optional. No Blank requirement disappears when it is absent, and no Superpowers workflow may override a higher Blank authority.
