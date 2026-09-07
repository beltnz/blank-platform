# AI COST AND PRACTICALITY REVIEW
## Blank Platform — Version 0.02.0

## Finding

This release deliberately reduces documentation volume while preserving authority. Rules repeated in several long forms were consolidated into one canonical home and referenced elsewhere.

## Cost Controls

- `AGENTS.md` + context map remain the normal agent entry.
- Documents distinguish capability/service/policy/delivery obligation to avoid treating every engineering concern as a new abstraction.
- Toolbox-first reuse and mature-contract immutability reduce repeated code generation.
- A missing reusable primitive requires user review; agents cannot invent infrastructure by reflex.
- Superpowers is optional and risk-scaled rather than automatically maximal-process.
- Model choice, context, delegation and tests are proportionate to risk.
- Optional technologies are deferred unless triggered.
- Document 06 is grouped into fewer, broader decision cards and the configurator supplies safe baseline defaults.

## Cost Must Not Weaken Assurance

Security/tenant/recovery/release gates retain required review/evidence. Cost optimization changes *how efficiently assurance is obtained*, not whether it is obtained.

## Measure After Concrete Stack Exists

Track context tokens, AI cost/task, first-pass success, rework, selected/full test runtime and high-risk review findings. Use evidence to tune workflow.
