# PLATFORM SECURITY MODEL
## Blank Production Application Platform — Version 0.02.0

# 1. Security Objective

Compromise, malformed input, dependency failure, operator mistake or malicious actor must not silently create unauthorized access, cross-tenant exposure, privilege escalation, secret disclosure, audit destruction or uncontrolled destructive change.

# 2. Principles

- default deny;
- least privilege;
- authentication != authorization;
- client/queue/event input is untrusted;
- tenant boundary is explicit;
- fail safely;
- stronger power requires stronger controls;
- production stricter than development;
- defense in depth;
- standard cryptography/protocols;
- security rules are tested.

# 3. Trust Boundaries

Treat browser/client, reverse proxy/edge, application runtime, database, queue, object store, external providers, CI/CD, administrative tooling and human operators as distinct trust boundaries. Trusted headers/context are accepted only from known upstream infrastructure.

# 4. Identity, Authentication and Sessions

Use mature authentication providers/libraries. Passwords use recognized adaptive hashing. Recovery is as security-sensitive as login. MFA/passkeys/elevated authentication are applied according to risk. Sessions have finite lifetime, rotation and revocation; privilege changes do not rely on stale sessions.

# 5. Authorization and Tenant Isolation

All protected actions pass centralized authorization. Tenant context comes from trusted membership/session state. Server-side query scoping is mandatory; RLS/database controls may add defense in depth. Wrong-tenant requests are tested permanently.

Do not map arbitrary external identity claims directly to privileged internal roles.

# 6. Privileged Operations

Platform administration, impersonation, break-glass, restore, migration, secret/key operations and Data Inspector are high-risk. Controls may include:

- explicit capability permission;
- recent strong auth/MFA;
- short-lived elevation;
- environment restriction;
- confirmation/reason;
- row/time/query limits;
- complete audit;
- independent review for material changes.

Tenant admin never implicitly equals platform admin.

# 7. Data Inspector

Normal users: no access. Tenant admins: no DB-level access by default. Development may be convenient; staging/production are progressively stricter. Direct SQL in production is disabled by default and requires separate explicit approval if enabled. Sensitive fields may be masked. Inspector cannot bypass authorization/audit/tenant policy.

# 8. Input, Browser and Edge Security

Validate all external input at trusted service boundaries. Reject invalid input; encode output according to context. Use deliberate CSRF, CORS, CSP/security headers, request-size limits and abuse/rate controls. Uploads are validated/scanned/isolation-treated according to risk.

If Apache/Cloudflare/load balancer fronts the app, define TLS termination and trusted forwarded-header sources explicitly. Never trust forwarded identity/IP/scheme headers from arbitrary clients.

# 9. Secrets, Keys and Cryptography

Secrets and keys use approved managed stores/mechanisms with least privilege and rotation where appropriate. Never place secret values in source, generated docs, ordinary logs or normal config UI. Cryptographic keys are conceptually separate from config. No bespoke cryptographic algorithms/protocols.

# 10. Persistence and Migration Security

Use parameterized/query-library primitives. Critical integrity uses constraints/transactions/version checks/locking as appropriate. Production migrations use trusted deployment identity, locking, traceability and destructive-change review. Ordinary users cannot trigger migrations.

# 11. Jobs, Events, Webhooks and Idempotency

Jobs/events carry explicit tenant/actor/correlation context but remain untrusted inputs to consumers. Validate type/version. Idempotency keys are bounded/scoped and cannot reveal another actor's result. Webhooks authenticate/sign, protect replay, use bounded retries and avoid duplicate effects.

# 12. Files and Exports

Object storage is private by default. Authorization precedes signed URL generation. URLs are short-lived and narrow. Untrusted uploads may require quarantine/malware scan. Sensitive exports may require reauthentication and are not permanently public.

# 13. Audit and Privacy

Audit history is protected from ordinary mutation. Capture enough accountability without unnecessary PII. Privacy deletion/anonymisation must reconcile retention, legal hold and audit integrity rather than blindly erasing history.

# 14. Dependencies and Supply Chain

Use an inventory/lockfile, vulnerability scanning, licence awareness and timely updates. Security-critical dependencies require maintenance/provenance scrutiny. Avoid unnecessary dependencies. Imported toolbox solutions receive the same review before approval.

# 15. CI/CD and Environment Security

Deployment pipelines are highly privileged: minimal permissions, protected branches, controlled secrets, authenticated deployment identity and audit/provenance where practical. Development/test/staging/production use separated data, secrets and credentials. Development credentials do not authenticate to production.

# 16. Backup, Restore and Recovery Security

Backups contain production data and require encryption, restricted access, retention/deletion policy and restore testing. Restore is privileged/destructive and needs authorization, controlled target, validation, audit and post-restore integrity checks. Recovery credentials must remain recoverable when the primary environment fails.

# 17. Safe Failure

Security-control uncertainty must not silently grant access. Examples:

- auth provider outage does not bypass authentication;
- authorization failure defaults deny;
- failed upload scan does not publish protected file;
- unavailable tenant context does not fall back global;
- failed secret provider does not use hard-coded fallback;
- production config cannot fall back to development fake provider.

# 18. Toolbox Gap Security Gate

Security-sensitive missing primitives are L3 Toolbox Gaps. The agent must stop before implementing custom auth, crypto, authorization, secret, tenant-isolation, audit, admin, database safety or similar reusable infrastructure. Present the gap and credible mature alternatives to the user. New bespoke code requires explicit user authorization and heightened review.

# 19. Canonical Security Invariants

1. Default deny.
2. Authentication and authorization remain separate.
3. Tenant isolation is enforced server-side.
4. UI/client state is not a security boundary.
5. Trusted context is established server-side.
6. Secrets are absent from source/logs/generated docs.
7. Passwords are never reversible.
8. No custom cryptography/auth protocols.
9. Public errors reveal no sensitive internals.
10. Audit history is protected from ordinary mutation.
11. Dangerous operations require explicit privilege.
12. Production Data Inspector is more restricted than development.
13. Direct SQL is production-disabled by default.
14. Cross-tenant tests are permanent.
15. Development powers do not silently exist in production.
16. Jobs/events are not trusted merely because internal.
17. Retry does not create uncontrolled duplicate effects.
18. Production migrations are privileged.
19. Backups/restores are protected like production data.
20. Security-critical toolbox gaps require user approval before new reusable code.

# 20. Additional Security Controls

These controls remain mandatory where applicable, even though they are compacted here:

- **Assurance levels:** ordinary, privileged and break-glass operations may require progressively stronger/recent authentication.
- **Session fixation/token rotation:** rotate identifiers after authentication/privilege changes; support global revocation according to policy.
- **Cross-tenant identifiers:** opaque IDs do not replace authorization; every lookup remains tenant/resource scoped.
- **Organisation units:** hierarchical scope cannot expand privilege beyond authorized tenant/resource context.
- **Service accounts/API consumers:** narrow non-human permissions, tenant scope, rotation and revocation.
- **Bulk Data Inspector:** bounded size/time, explicit permission, audit and protected-state enforcement.
- **Encryption at rest/application-level encryption:** use provider/platform encryption by default; application field encryption only for a demonstrated classification/threat need with managed keys.
- **Hashing vs encryption:** one-way credentials use hashing; reversible protection is used only when later plaintext recovery is a real requirement.
- **PII handling:** collection, logging, export and masking follow classification/minimisation policy.
- **Output encoding/SQL injection/SSRF:** encode for destination context; parameterize queries; restrict outbound schemes/hosts/networks where server-side fetching exists.
- **Uploaded file serving/CDN:** separate untrusted content where useful, use safe content headers/types, avoid executable interpretation.
- **Brute force/IP blocks/bot detection/honeypots:** use risk-based abuse controls; do not create accessibility/usability denial without evidence.
- **Notification security:** recipients/templates/variables are authorized; sensitive content is minimized; provider failure does not leak secrets.
- **Search/cache security:** tenant/authorization scope is preserved in indexes/cache keys; cache collision/staleness cannot expose another principal's data.
- **API version security:** deprecated versions do not retain known insecure behaviour indefinitely.

# 21. Failure and Incident Behaviour

Explicitly define safe behaviour for failure of identity provider, authorization, configuration, flags, secret store, audit pipeline, logging, malware scanner and rate limiter. Failure must be observable. Availability trade-offs that weaken a security boundary require approved policy, not an ad-hoc fallback.

Incident containment may use kill switches, session revocation, credential/key rotation, traffic restriction, read-only/maintenance mode and provider isolation. Security alerts correlate with audit/request/build identity where practical.

# 22. Security Lifecycle

- Security review is risk-triggered, not mandatory fan-out for every trivial change.
- Permanent authz/cross-tenant/session/Data Inspector/file/API tests protect critical boundaries.
- Security ADR is required for material trust-boundary or invariant changes.
- Temporary security exceptions are documented, time-bounded, owned and have removal conditions.
- Patch/vulnerability handling has ownership and severity-based urgency.
- Vulnerability disclosure/contact mechanism exists when public deployment requires it.
- Secure debugging avoids exposing production secrets/PII or weakening authorization.
- Human override does not bypass canonical security without explicit approved exception.

## Superpowers compatibility

**IF Superpowers is being used:** use applicable Superpowers skills as the execution method, subject to Blank authority, risk, cost, toolbox, contract, security and verification rules.

**ELSE:** use the native Blank workflow in `08_AI_ENGINEERING_OPERATING_MODEL.md`.

Superpowers is optional. No Blank requirement disappears when it is absent, and no Superpowers workflow may override a higher Blank authority.
