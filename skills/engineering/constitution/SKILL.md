---
name: constitution
version: 1.0.0
author: Mike (Mycroft Holmes) for trippydao
license: MIT
platforms: [linux]
metadata:
  hermes:
    tags: [sdd, spec, workflow, agents]
    related_skills: [ask-matt, to-spec, to-tickets, implement, wayfinder]
description: Use when creating a code repo — constitution-first SDD loop.
---

# Constitution — standing context for a code project

The constitution is the project-level spec: mission, stack constraints, roadmap. It is the standing artifact every feature spec reads from. Feature skills (to-spec, to-tickets, implement) are per-feature; this is the layer that survives between them.

## When to Use

- New repo or project → write the constitution BEFORE feature work.
- Existing repo without one → reverse-engineer from README, CONTEXT.md, ADRs, git log; the owner corrects; commit.
- Exception: throwaway prototypes. No constitution for `/prototype` output.

## The artifact: `spec/constitution.md`

Three sections:

1. **Mission** — why the project exists, who it serves, in-scope and (explicitly) out-of-scope.
2. **Stack & constraints** — the non-negotiables: language, frameworks, infra, package manager, sovereign-stack rules. One line each. Test for inclusion: would changing this one line ripple through hundreds of lines of code?
3. **Roadmap** — phases in order, current phase marked. Living doc.

Discipline:

- Decisions live in the constitution. Agent rules (build commands, test commands, style rules) stay in AGENTS.md, which points at the constitution.
- Specs are committed with the code. Which spec version produced which change is visible in git history.
- Constitution edits: trivial → same commit as the work. Structural → own commit (or branch), noted in the changelog.

## The loop

1. **Constitution current?** If not, update it first.
2. **Per feature**: grill(-with-docs) → `to-spec` → `to-tickets` → `implement` (tdd inside, code-review on the diff). A feature spec that contradicts the constitution stops: amend the constitution explicitly first, never let the spec drift it silently.
3. **Between features (replanning)**: mark the phase done, re-check the roadmap. Side-ideas → dated research note (`spec/research/YYYY-MM-DD-slug.md`) + one-line roadmap pointer. Not a context detour.
4. **MVP test**: when the build looks done, run the remaining roadmap from constitution + specs alone. Divergence = spec defect first, code defect second.

## Subagent handoff contract

For delegate/subagent builds: the goal names the constitution path and the feature spec path. Fresh context, branch per feature. At the end: diff-vs-spec review, then a subagent deep-review for large diffs (protects the main context window).

## Pitfalls

- Don't constitution trivial scripts or prototypes.
- Constitution ≠ AGENTS.md: decisions vs rules. Don't merge them.
- Don't write specs the constitution can't see — orphan specs decay exactly like unsaved dialogue.
