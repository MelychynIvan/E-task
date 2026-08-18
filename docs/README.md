# E-task documentation index

This directory is the durable project context for human developers and coding agents such as Codex.

## Required reading order for Codex

1. `/AGENTS.md` — repository-wide operating rules and context map.
2. `/docs/product/PRODUCT_SPEC.md` — current product requirements and UX behavior.
3. `/docs/product/DECISIONS.md` — dated decisions; newer confirmed decisions override older conflicting product text.
4. `/docs/CODEX_WORKFLOW.md` — how to plan, implement, test, document and ask questions.
5. Relevant code and tests for the task being implemented.

## Source-of-truth model

- The user’s current explicit instruction always wins.
- More specific `AGENTS.md` files, if added later inside subdirectories, apply to their directory tree.
- Confirmed dated decisions in `docs/product/DECISIONS.md` override older conflicting documentation.
- `docs/product/PRODUCT_SPEC.md` is the local repository mirror of the Master Product Spec and should be kept synchronized after confirmed product changes.
- Existing implementation does not automatically become a product requirement. If code conflicts with the confirmed spec, fix the code rather than silently changing the product.

## Documentation maintenance rule

When a task introduces or confirms a product/architecture decision:

1. Update `docs/product/DECISIONS.md` with the date and decision.
2. Update `docs/product/PRODUCT_SPEC.md` if the decision changes the product contract.
3. Update `AGENTS.md` only if the decision changes repository-wide working rules.
4. Do not leave contradictory instructions in different documents.

## Current repository

- Repository: `MelychynIvan/E-task`
- Default branch: `main`
- Active initial development branch: `codex/initial-app-scaffold`
- Current product working name: `E-task` until a final name is approved.
