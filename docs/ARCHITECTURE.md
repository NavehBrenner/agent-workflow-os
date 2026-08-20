# Architecture (early sketch)

This is an initial shape, not a final design. It exists so we have a shared reference while we discuss the real interfaces.

## High-level components

```
┌─────────────────────────────────────────────────────────┐
│                     Agent (Claude Code)                 │
│  loads standing policy + can call local helpers         │
└───────────────────────────┬─────────────────────────────┘
                            │
         ┌──────────────────┼──────────────────┐
         ▼                  ▼                  ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│ Local Surface   │ │ Discovery       │ │ Reflection      │
│ - scripts/      │ │ - curated       │ │ - harvest       │
│ - aliases       │ │   registries    │ │   successful    │
│ - local skills  │ │ - propose/      │ │   workflows     │
│ - small index   │ │   install gate  │ │ - create/       │
│                 │ │                 │ │   improve       │
└─────────────────┘ └─────────────────┘ └─────────────────┘
         │                  │                  │
         └──────────────────┼──────────────────┘
                            ▼
              Standing Policy (skill / instructions)
              "local first → gated discovery →
               efficient execution → reflect"
```

## 1. Standing Policy

The primary control surface in v0.

- Delivered as one or more skills (and optionally a CLAUDE.md fragment) installed by the bootstrap command.
- Expresses the 4-step loop clearly and briefly.
- Points the agent at the local index and the discovery helpers.
- Does **not** try to be a full runtime enforcer.

## 2. Local Surface

Owned directories and conventions:

- Project scripts (candidates: `.agent/scripts/`, `bin/`, or similar)
- Project-local skills (standard `.claude/skills/` or equivalent)
- Optional user-level scripts/aliases
- A cheap-to-read index (names + one-line descriptions + type)

The agent should be able to list the local surface with minimal tokens.

## 3. Discovery

- Thin helpers (skill or small CLI) that know how to query a small allowlist of registries.
- Output is ranked / filtered proposals, not raw dumps.
- Install path is explicit and logged.
- Default policy: propose, do not auto-apply unless configured otherwise.

## 4. Reflection

- Triggered by the agent under the standing policy after suitable successful work.
- Produces candidates for new or improved local scripts/aliases/skills.
- Writes into the Local Surface and updates the index.
- Should explain the change in the session.

## 5. Bootstrap / Install

One command that:

1. Writes the standing policy skill(s)
2. Ensures the local directories exist
3. Seeds a minimal index
4. Optionally registers trusted registries / discovery helpers
5. Documents the contract for the human and the agent

## Open design questions (to discuss next)

- Exact directory conventions and naming
- Shape of the local index (file format, how the agent reads it)
- How aggressive reflection should be in v0
- Concrete trust model and confirmation UX for installs
- Whether any host-specific hooks are worth using early
- Minimal viable bootstrap command surface

These will be resolved in further design discussion and then reflected back into this document and SPEC.md.
