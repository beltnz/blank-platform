# Blank Platform Technology Configurator

Version 0.9.0 — aligned with Blank v0.02.0.

## What changed

- Reads external Blank Documents `00`–`08` plus `06A`; no framework documents are embedded.
- Document 06 is now intentionally condensed into grouped decision cards rather than hundreds of narrowly split cards.
- Quick Start + safe baseline remains the normal low-input workflow.
- Existing/partial project 06 files can still be loaded and overlaid onto the pristine current Blank 06.
- Mature-contract/toolbox hard gate and optional Superpowers IF/ELSE behaviour remain.
- Generated capability registry now distinguishes `foundation-capability` from `platform-service`.
- New `PROJECT_DELIVERY_OBLIGATIONS.md` separates production evidence from reusable capability inventory.

## Framework folder expected

```text
00_BLANK_PLATFORM_MANIFESTO.md
01_CANONICAL_PLATFORM_ARCHITECTURE.md
02_AI_DEVELOPMENT_CONSTITUTION.md
03_PLATFORM_CAPABILITY_CONTRACTS.md
04_PLATFORM_SECURITY_MODEL.md
05_BLANK_PLATFORM_DEFINITION_OF_DONE.md
06_TECHNOLOGY_IMPLEMENTATION_SPECIFICATION_TEMPLATE.md
06A_TECHNOLOGY_IMPLEMENTATION_RECIPE.md
07_DEVELOPMENT_TEST_DATA_AND_VERIFICATION_MODEL.md
08_AI_ENGINEERING_OPERATING_MODEL.md
```

The pristine framework 06 is never modified. Resume work with `PROJECT_TECHNOLOGY_IMPLEMENTATION_SPECIFICATION.partial.md`.

## Generated project bundle

```text
PROJECT_TECHNOLOGY_IMPLEMENTATION_SPECIFICATION.md
PROJECT_AGENTS.md
PROJECT_AGENT_CONTEXT_MAP.yaml
PROJECT_TECHNOLOGY_PROFILE.yaml
PROJECT_DEVELOPMENT_COMMANDS.md
PROJECT_ENVIRONMENT_MATRIX.yaml
PROJECT_PLATFORM_CAPABILITY_REGISTRY.yaml
PROJECT_TOOLBOX_REGISTRY.yaml
PROJECT_TOOLBOX_POLICY.md
PROJECT_DELIVERY_OBLIGATIONS.md
PROJECT_AI_COST_AND_PRACTICALITY_REVIEW.md
PROJECT_BOOTSTRAP_MANIFEST.yaml
AGENTS.md
```

## Core governance

IF Superpowers is available/enabled, its skills operate under Blank Document 08. ELSE native Blank workflow applies. Mature toolbox/contracts are reused first. A genuine missing reusable primitive requires user approval before bespoke code or contract expansion.
