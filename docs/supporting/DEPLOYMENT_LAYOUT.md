# DEPLOYMENT LAYOUT — ELI5
## Blank Platform — Version 0.02.0

Keep reusable Blank rules separate from generated project answers.

```text
MY_PROJECT/
├── AGENTS.md                         # tiny AI entry point
├── src/
├── tests/
├── infrastructure/
├── scripts/
└── blank/
    ├── framework/                    # reusable Blank source — keep clean
    │   ├── 00_BLANK_PLATFORM_MANIFESTO.md
    │   ├── 01_CANONICAL_PLATFORM_ARCHITECTURE.md
    │   ├── 02_AI_DEVELOPMENT_CONSTITUTION.md
    │   ├── 03_PLATFORM_CAPABILITY_CONTRACTS.md
    │   ├── 04_PLATFORM_SECURITY_MODEL.md
    │   ├── 05_BLANK_PLATFORM_DEFINITION_OF_DONE.md
    │   ├── 06_TECHNOLOGY_IMPLEMENTATION_SPECIFICATION_TEMPLATE.md
    │   ├── 06A_TECHNOLOGY_IMPLEMENTATION_RECIPE.md
    │   ├── 07_DEVELOPMENT_TEST_DATA_AND_VERIFICATION_MODEL.md
    │   └── 08_AI_ENGINEERING_OPERATING_MODEL.md
    └── project/                      # generated facts for THIS project
        ├── PROJECT_TECHNOLOGY_IMPLEMENTATION_SPECIFICATION.md
        ├── PROJECT_AGENTS.md
        ├── PROJECT_AGENT_CONTEXT_MAP.yaml
        ├── PROJECT_TECHNOLOGY_PROFILE.yaml
        ├── PROJECT_PLATFORM_CAPABILITY_REGISTRY.yaml
        ├── PROJECT_TOOLBOX_REGISTRY.yaml
        ├── PROJECT_TOOLBOX_POLICY.md
        ├── PROJECT_DELIVERY_OBLIGATIONS.md
        ├── PROJECT_DEVELOPMENT_COMMANDS.md
        ├── PROJECT_ENVIRONMENT_MATRIX.yaml
        └── PROJECT_BOOTSTRAP_MANIFEST.yaml
```

ELI5: `blank/framework` says **what Blank means**. `blank/project` says **how this project implements it**. Root `AGENTS.md` tells the AI where to start.
