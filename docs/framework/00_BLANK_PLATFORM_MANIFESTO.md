# THE BLANK PLATFORM MANIFESTO
## Blank Production Application Platform — Version 0.02.0

# 1. Purpose

Blank is a reusable production foundation for internet-facing applications. It is **operationally complete, but semantically empty**: it supplies recurring infrastructure and engineering rules without knowing the business domain.

Build recurring foundations once; expose stable contracts; test them hard; reuse them as internal black boxes. Domain code should consume known interfaces rather than repeatedly reconstruct authentication, tenancy, authorization, persistence rules, configuration, audit, jobs, files, observability, administration, recovery or security controls.

# 2. Why Blank Exists

AI-assisted development magnifies both reuse and drift. Without explicit boundaries, agents repeatedly rediscover settled decisions, duplicate utilities, bypass abstractions, weaken security or rewrite mature code. Every rediscovery costs tokens, review, tests and future comprehension.

Blank therefore optimizes for:

- secure-by-default production behaviour;
- stable, testable internal contracts;
- minimal repeated reasoning;
- mature mainstream technology;
- additive domain extension;
- small, targeted agent context;
- lowest practical lifetime cost consistent with required assurance.

# 3. Four Kinds of Blank Requirement

Blank distinguishes four things that are often mixed together:

1. **Foundation Capability** — reusable interface consumed by application/platform code, e.g. authorization, validation, persistence semantics, configuration, audit, jobs.
2. **Platform Service** — reusable operational mechanism, e.g. notifications, object storage, health/readiness, feature flags.
3. **Cross-Cutting Policy** — rule that applies across capabilities, e.g. tenant isolation, safe failure, idempotency, immutable mature contracts, toolbox-first reuse.
4. **Delivery Obligation** — evidence every concrete application must provide before production, e.g. restore proof, RPO/RTO, rate-limit assessment, lifecycle policy, security verification.

A concern may be both a reusable mechanism and a delivery obligation. Importance alone does not make something a foundation capability.

# 4. Internal Black Boxes and Contracts

A mature capability should behave like an internal API. Consumers need its purpose, inputs, outputs, errors, permissions, side effects and guarantees; they should not need implementation internals.

The dependency direction is:

```text
Domain -> Platform Contracts -> Platform Implementations -> Infrastructure
```

Platform code must not depend on domain code. Domain modules extend through approved registration/extension points rather than invasive core modification.

# 5. Mature Means Immutable by Default

A contract/component is **mature** when its public behaviour is documented, stable, tested and registered as an approved toolbox capability. Mature does not mean physically unchangeable; it means **not casually changeable**.

Agents must prefer, in order:

1. existing mature contract/tool;
2. approved extension point;
3. composition of existing tools;
4. approved external mature solution;
5. only then, explicitly authorised new reusable code.

Examples:

- If the UI library already has a modal/dialog primitive, do not invent another.
- If the selected data layer already has an insert primitive, do not create `BlankDatabase.insert()` merely to wrap it.
- Blank owns the canonical semantics around tenant scope, transactions, errors, authorization and observability; it need not duplicate adequate library primitives.

# 6. Toolbox Gap Rule

A feature request is **not permission to manufacture missing reusable infrastructure**.

When a needed reusable primitive is absent:

```text
Search approved toolbox and mature contracts
        ↓
Found? -> reuse it
        ↓ no
STOP and present the gap to the user
        ↓
User may research GitHub/packages/other mature solutions
        ↓
User chooses reuse/import/compose/extend/change-contract/new-code/defer
        ↓
Proceed only with that decision
```

External code still requires security, maintenance, licence, compatibility and supply-chain review. Ordinary domain-specific code that uses existing capabilities does not require this gap approval; **new reusable primitives, infrastructure or mature-contract changes do**.

# 7. Security and Production Reality

Blank assumes an internet-facing threat model. Authentication is not authorization. Authorization defaults to deny. Tenant isolation is server-enforced. UI visibility is never a security boundary. Secrets do not belong in source or logs. Dangerous operator functions require stronger controls than ordinary use. Production is stricter than development.

Security claims must be enforceable and testable, not merely documented.

# 8. Engineering Economy

Cost is an engineering constraint:

```text
AI cost ≈ model price × context volume × iterations × agent count
```

Use the cheapest model expected to succeed reliably, minimum relevant context, affected tests first, risk-scaled review, and specialist/subagent work only where it materially reduces error. Cheap work must not reduce required assurance.

# 9. Foundational Bargain

> We constrain how foundational infrastructure changes so teams gain greater freedom, speed and safety when building actual products.

The goal is not the most elaborate platform. It is a coherent, secure, boring foundation that becomes cheaper to use over time.

## Superpowers compatibility

**IF Superpowers is being used:** use applicable Superpowers skills as the execution method, subject to Blank authority, risk, cost, toolbox, contract, security and verification rules.

**ELSE:** use the native Blank workflow in `08_AI_ENGINEERING_OPERATING_MODEL.md`.

Superpowers is optional. No Blank requirement disappears when it is absent, and no Superpowers workflow may override a higher Blank authority.

# 10. Reading Order

Humans: Manifesto -> Architecture -> Operating Model, then relevant contracts/security/technology documents.

AI agents: start at `AGENTS.md`; load only routed material. Cross-references are locators, not instructions to read everything recursively.
