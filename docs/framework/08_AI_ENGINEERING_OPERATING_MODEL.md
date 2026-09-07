# AI ENGINEERING OPERATING MODEL
## Blank + Optional Superpowers Cooperation — Version 0.02.0

# 1. Purpose

This document selects **how much process, model capability, context, testing and review a task deserves**. It coordinates Blank with Superpowers when present while keeping Blank complete when absent.

# 2. Precedence

```text
Blank security invariants
Blank canonical architecture
ADRs
Mature contracts
Project technology decisions
This operating model
Superpowers skills/workflows
Task plan
Agent preference
```

Superpowers controls execution method, not architecture authority.

# 3. Conditional Workflow

**IF Superpowers is being used:** select only applicable skills and apply them at the risk level below. Superpowers' own workflow may be thorough; Blank may skip redundant fan-out/ceremony only when equivalent assurance is preserved.

**ELSE:** use the native steps listed for the same execution mode.

No requirement is conditional on Superpowers availability.

# 4. Execution Modes

## Mode A — Micro
Typos, CSS spacing, rename, isolated pure fix.

Native: understand -> change -> cheap affected check -> verify. No mandatory brainstorm/design/subagent.

## Mode B — Normal
Bounded feature/change within established contracts.

Native: brief clarification -> short plan -> implement -> tests for changed behaviour -> self-review -> verify.

## Mode C — High Risk
Auth/authz/tenancy/session/secrets/migrations/audit/Data Inspector/destructive/concurrency/security boundary.

Native: explicit design/threat review -> plan -> isolated change -> TDD/contract tests -> independent security/spec review -> relevant integration/security evidence.

## Mode D — Architectural
New platform capability, mature contract change, new reusable primitive, deployment topology/database architecture/breaking public contract.

Native: L2/L3 review and human approval -> ADR/design -> toolbox-gap decision if applicable -> implementation plan -> high-assurance execution/review -> broad verification.

# 5. Model Selection

Use the cheapest model expected to complete the task reliably. Escalate for architecture/security/ambiguous debugging or after a cheaper model demonstrably fails. Do not pay premium-model cost for mechanical search/rename/boilerplate.

# 6. Delegation Budget

Do not spawn children to summarize settled docs, reread architecture, review trivial L0/L1, or perform research unable to change a decision. Delegate only independent parallel work or high-risk verification. Pass minimum context.

# 7. Verification Budget

Map Mode A/B/C/D to T0–T4 in Documents 02/07. A second independent reviewer is normally unnecessary for Mode A/B unless risk changes. High-risk findings justify the extra spend.

# 8. Toolbox Gap Overrides Workflow

At any mode, if the agent needs a reusable tool not in the approved toolbox/contracts/framework/dependencies, **stop before creating it**. Present the gap to the user. The user may research GitHub/packages and decide import/compose/extend/contract-change/new-code/defer. This is L3 and cannot be bypassed by Superpowers brainstorming/planning or by task wording.

# 9. Stop Rules

Stop research when hard requirements are satisfied and more options are unlikely to change the decision. Stop refactoring when contract is satisfied, tests pass and no material maintainability/security defect remains. Do not keep reviewing after independent review passes unless code materially changed.

# 10. Measurement

Where practical track tokens/cost per merged task, first-pass success, rework, test runtime, review findings and context size by task class. Tune process empirically while preserving assurance.
