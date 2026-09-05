# Adaptations from upstream

Upstream: https://github.com/mattpocock/skills (remote `upstream`)
This fork is the flavor layer. Every deliberate divergence from upstream is listed here. If a divergence is not listed, treat it as drift to be resolved by re-syncing from upstream.

## Sync procedure

1. `git fetch upstream`
2. `git merge upstream/main` (fork main tracks upstream main; no squash)
3. Re-apply anything in this file that the merge clobbered (each entry names the files it touches).
4. Push to origin.

## Standing adaptations

| # | Divergence | Files | Why |
|---|-----------|-------|-----|
| 1 | Tracker setup pointer rewritten: `tell the user to run /setup-matt-pocock-skills` → `default to the local-markdown tracker and tell the user to configure one (see setup-matt-pocock-skills)` | `skills/engineering/code-review/SKILL.md`, `to-spec`, `to-tickets`, `wayfinder`, `triage` | Hermes stack runs its own tracker convention (GitHub Issues + kanban via gh CLI); the setup skill's Claude-Code-specific flow is a fallback, not the default. |
| 2 | `productivity/grill-me` and `productivity/handoff` are ours, not upstream's | `skills/productivity/grill-me/`, `skills/productivity/handoff/` | Both are heavily flavored for the Hermes stack (grill-me: check-the-system-before-asking loop, execution-phase tracking; handoff: multi-surface Mike/Honcho, no-doc pickup, redaction). Upstream versions are thinner generics. On merge conflicts here, **ours wins** — do not take upstream. |

## Non-adaptations (deliberately not adopted)

- **docs/ publishing pipeline** (aihero.dev URLs, docs tree, install block): we don't publish the fork. The *discipline* (per-skill what-it-does / when-to-reach-for-it page) is adopted as vault notes, not repo docs.
- **`.claude-plugin` / changesets / release machinery**: harness is Hermes, not Claude Code plugin distribution.
- **No-em-dash prose rule**: upstream house style, not ours.
- **Never-name-the-author convention**: public-facing rule; our vault keeps provenance.

## Provenance note

The Hermes live skill library (`~/.hermes/skills/`) predates this fork and contains older snapshots of several of these skills, plus independent skills from obra/superpowers and elsewhere. This fork is the upstream-tracking source for the engineering workflow set; porting fork → `~/.hermes/skills/` is a separate, deliberate step per skill (the live library has its own flavors that must not be clobbered).
