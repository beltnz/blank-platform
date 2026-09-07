# Blank Platform

**Operationally complete. Semantically empty.**

Blank is a production-ready, domain-neutral foundation for building internet-facing applications, especially with AI coding agents.

It provides the common parts serious applications need before business rules are added: identity, security, tenants, permissions, persistence rules, validation, configuration, audit, jobs, files, notifications, observability, administration, deployment guidance, testing, recovery, and more.

> **Build the foundations once. Reuse them. Do not ask every project—or every AI agent—to invent them again.**

## Why Blank exists

Most applications repeatedly rebuild the same basic machinery.

That costs developer time. With AI-assisted development, it also costs tokens, agent time, review effort, and repeated reasoning. Rebuilding security and infrastructure for every project also creates new chances for mistakes.

Blank takes a different approach.

Common application foundations are defined once through clear contracts, policies, guardrails, and implementation decisions. Mature components are then treated as known tools with stable interfaces. The business application is built on top.

Blank calls this:

> **Operationally complete, but semantically empty.**

It should know how to run a serious application without knowing what that application is *about*.

## What Blank is

Blank is both an **architecture** and an **engineering rulebook**.

It defines:

- reusable foundation capabilities and platform services;
- contracts between the platform and application code;
- security rules that must not be weakened;
- rules for data, tenants, permissions, secrets, validation, jobs and other shared concerns;
- what a production application must prove before release;
- how technology choices are made;
- how testing and verification are performed;
- how AI coding agents should work within the architecture; and
- when an agent must stop and ask a human rather than invent new infrastructure.

Blank is **technology-neutral at its core**. A separate implementation specification turns it into a concrete stack for a real project.

## What Blank is not

Blank is not a finished business application.

It does not decide whether you are building a booking system, club portal, CRM, shop, school application, SaaS product, or something else.

It is also not permission to create a large custom framework.

Where a mature library, framework, database, provider, or existing project component already solves a problem well, Blank prefers to use it.

For example, Blank may define required rules around persistence, tenant isolation, transactions and errors. It should not create another generic `insert()` function merely because the selected database library already has one.

## The toolbox rule

One of Blank's strongest rules is:

> **Reuse before invention.**

When development needs reusable functionality:

1. Check the approved toolbox and mature contracts.
2. Reuse an existing solution where it fits.
3. Prefer composition or an approved extension point where possible.
4. Consider a mature external library or existing solution where appropriate.
5. If the toolbox genuinely cannot meet the need, **stop and present the gap to the user**.
6. Do not create new reusable infrastructure until the user approves what should happen.

A feature request is **not** automatic permission for an AI agent to invent a new framework component.

This protects consistency, security, maintainability, and AI cost.

## Capabilities and obligations are different

Blank separates four kinds of requirements:

| Type | Meaning |
|---|---|
| **Foundation Capability** | Reusable machinery applications can depend on. |
| **Platform Service** | A shared operational service supplied by the platform. |
| **Cross-Cutting Policy** | A rule that applies across several parts of the system. |
| **Delivery Obligation** | Something each real application must prove before production. |

This distinction matters.

Health checking, for example, can use a reusable platform service, but every deployed application must still prove its health and readiness checks work.

Backup and disaster recovery are essential, but the release question is not simply, "Does a backup API exist?" It is, "Can this application actually be restored within its agreed recovery targets?"

## Security is part of the foundation

Security is not an optional finishing step.

Blank defines rules for authentication, sessions, authorization, tenant isolation, validation, secrets, audit, privileged administration, data protection, abuse protection, safe failure, dependencies, backup and recovery, and production access.

Security-sensitive rules take precedence over local convenience.

## Built for AI-assisted development

Blank was designed with AI coding agents in mind.

Agents should not need to rediscover the architecture on every task. Blank therefore provides explicit contracts, context routing, decision levels, protected boundaries, verification rules, and a controlled toolbox.

The aim is not to make an agent read every document before changing one line of code. Normal context should be only what the task needs:

**task + agent instructions + relevant contract + affected code/tests + any triggered security or architecture rule**

Blank also discourages unnecessary agents, repeated research, redundant reviews, and documentation churn.

A useful approximation is:

> **AI cost ≈ model cost × context size × iterations × agent count**

Good architecture should reduce all four.

## Superpowers is optional

Blank can work with the **Superpowers** coding-agent methodology, but does not depend on it.

If Superpowers is enabled, its relevant skills and workflows may control **how work is carried out**.

If it is not enabled, Blank's native engineering workflow is used.

In either case, Blank's architecture, security rules, contracts, approved technology choices, and toolbox rules remain authoritative.

> **Superpowers may decide how work is carried out. Blank decides what the system is allowed to become.**

## Repository guide

```text
blank-platform/
├── README.md
├── LICENSE
├── AGENTS.md
├── AGENT_CONTEXT_MAP.yaml
├── docs/
│   ├── framework/
│   │   ├── 00_BLANK_PLATFORM_MANIFESTO.md
│   │   ├── 01_CANONICAL_PLATFORM_ARCHITECTURE.md
│   │   ├── 02_AI_DEVELOPMENT_CONSTITUTION.md
│   │   ├── 03_PLATFORM_CAPABILITY_CONTRACTS.md
│   │   ├── 04_PLATFORM_SECURITY_MODEL.md
│   │   ├── 05_BLANK_PLATFORM_DEFINITION_OF_DONE.md
│   │   ├── 06_TECHNOLOGY_IMPLEMENTATION_SPECIFICATION_TEMPLATE.md
│   │   ├── 06A_TECHNOLOGY_IMPLEMENTATION_RECIPE.md
│   │   ├── 07_DEVELOPMENT_TEST_DATA_AND_VERIFICATION_MODEL.md
│   │   └── 08_AI_ENGINEERING_OPERATING_MODEL.md
│   └── supporting/
│       ├── AI_COST_AND_PRACTICALITY_REVIEW.md
│       ├── DEPLOYMENT_LAYOUT.md
│       ├── MAJOR_UPDATE_REVIEW_REPORT.md
│       └── TOOLBOX_GAP_DECISION_TEMPLATE.md
├── tools/
│   └── configurator/
│       ├── index.html
│       └── README.md
└── metadata/
    └── DOCUMENT_SET_MANIFEST.json
```

### Where should I start?

For a human reader:

1. Read **`00_BLANK_PLATFORM_MANIFESTO.md`** to understand why Blank exists.
2. Read **`01_CANONICAL_PLATFORM_ARCHITECTURE.md`** to understand the system.
3. Use **`06A_TECHNOLOGY_IMPLEMENTATION_RECIPE.md`** when turning Blank into a real technology stack.
4. Use the browser configurator in **`tools/configurator/`** to help make and record those technology decisions.

For an AI coding agent, start with **`AGENTS.md`** and **`AGENT_CONTEXT_MAP.yaml`**. They route the agent to the smallest useful set of authoritative documents.

## From Blank to a real application

Blank separates three stages:

```text
Generic Blank
     ↓
Choose and record the technology stack
     ↓
Concrete, stack-specific Blank
     ↓
Add business/domain requirements
     ↓
Real application
```

Domain requirements should not leak backwards into the generic Blank foundation. This allows the same foundation to support many different applications.

## Production readiness

Blank does not treat "it works on my machine" as production readiness.

A release must provide evidence for the obligations that apply to it, including security, tenant isolation, validation, migrations, testing, backup and restore, health and readiness, operational resilience, observability, data lifecycle, and deployment.

Where an obligation genuinely does not apply, it should be marked **N/A with a reason**, rather than silently ignored.

> **Production readiness is not a feeling. It is evidence.**

## Current status

Blank is under active development.

The current foundational document set is **v0.02.0**. The technology configurator is **v0.9.0**.

The project is suitable for review, experimentation, architecture work, and implementation planning. Versions below `1.0` mean that contracts, document structure, and tooling may still change.

## Licence

Blank Platform is licensed under the **Apache License 2.0**.

It may be used in open-source and commercial projects subject to the licence terms. See [`LICENSE`](LICENSE).

## Core idea

Blank is based on a simple trade:

> **Constrain the foundation so the application can be free.**

Authentication, permissions, persistence rules, validation, secrets, audit, jobs, deployment, recovery and similar infrastructure should not need to be rediscovered for every new product.

Build those foundations carefully. Give them stable contracts. Reuse mature tools. Protect the important boundaries.

Then let developers—and AI agents—spend their effort on what makes the application different.
