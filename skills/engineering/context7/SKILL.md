---
name: context7
version: 1.0.0
description: Use when code answers hinge on library APIs or versions.
---

# Context7 — current library docs on demand

The `ctx7` CLI + this skill replace the Context7 MCP server (CLI+skill pattern — lighter setup, less context). Current upstream docs for any library, with source links.

## When to Use

- Grilling, spec-writing, or implementing when an answer about an external library's API, config flag, or version matters.
- Any time you would otherwise answer a library question from model memory. Memory is stale; this is not.

## Flow

1. Resolve the library:

   ```
   bunx ctx7 library <name>
   ```

   Pick the `/org/repo` ID with high Source Reputation and the version range matching the project's pin.

2. Query it:

   ```
   bunx ctx7 docs <library-id> "<specific question>"
   ```

3. Cite what you got. If docs contradict the plan, surface it — do not silently reconcile.

## Auth

Anonymous use works (rate-limited). `ctx7 whoami` checks status; `ctx7 login` is an optional device-flow for higher limits — the owner runs it, never automated.

## Pitfalls

- Do not use it for our own repos' internals — vault, mike-infra, fork skills. It serves upstream public docs only.
- Docs are current upstream; our pinned versions may differ. Match the version when picking the library ID.
- Query one specific question per call. Do not dump whole doc trees into context.
- `bunx ctx7 upgrade` exists; bun caches the binary, so no global install and no npm globals.
