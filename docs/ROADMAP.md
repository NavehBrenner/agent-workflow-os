# Roadmap (initial)

Phased so that each stage is useful on its own and does not require the full vision.

## Phase 0 — Design foundation (current)

- Vision, SPEC, PROBLEMS, ARCHITECTURE documents
- Agree on how we tackle the hard problems
- Freeze a narrow v0 scope

## Phase 1 — Local-first core

Goal: after install, the agent reliably prefers and reuses a local deterministic surface.

- Bootstrap command that installs standing policy + local directories + empty index
- Conventions for scripts / aliases / local skills
- Standing policy that makes local-first the default behavior
- Manual or agent-assisted creation of the first few scripts/aliases (including the classic rebase-main style example)
- Basic list / show of the local surface

Success: on the author's real repos, recurring shell sequences start becoming short names that the agent actually uses.

## Phase 2 — Conservative discovery

Goal: the agent can find and (safely) bring in external skills when local capability is missing.

- Small allowlist of registries
- Discovery helper the agent can call
- Propose + confirm install flow
- Recording of what was installed

Success: external skills are added only with visibility and control, and they are useful when added.

## Phase 3 — Reflection loop

Goal: successful recurring workflows produce lasting local improvements without human busywork.

- Clear trigger conditions for reflection
- Creation / improvement of scripts, aliases, and simple skills
- Index updates and basic hygiene (prefer improve over duplicate)

Success: the local surface grows usefully over a few weeks of real use, not just noise.

## Phase 4 — Hardening and optional expansion

- Better pruning / audit
- Stronger measurement of whether the system is helping
- Optional host-specific accelerators (hooks, plugins)
- Consider additional agents only after the Claude Code path is solid

## Explicit non-goals for early phases

- Universal multi-agent support
- Fully automatic unattended external installs
- Perfect compliance guarantees
- Competing with full agent frameworks or IDEs
