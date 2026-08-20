# agent-workflow-os

**Single-install layer that lets coding agents manage their own skills, scripts, aliases, discovery, and reflection.**

Install once into a repo. From that point the agent should:

1. Prefer existing local skills / scripts / aliases when they cover the task
2. Discover useful external skills and install them (conservatively)
3. Orchestrate helpers and subagents for good results with low context/token cost
4. Reflect after workflows and create or improve local skills, scripts, and aliases

The goal is to remove the ongoing burden of agent workflow management from the human, so that starting a new project becomes roughly "two installs" (this + a code-quality harness) and then the agent can work with minimal friction.

> **Status**: Early design / pre-implementation. Specs and problem analysis are being written. No working runtime yet.

## Why this exists

Coding agents already have many building blocks:

- Skills / slash commands / subagents
- Shell and git aliases
- CLI wrapper scripts as tools
- Skill marketplaces and install CLIs
- Self-improving / harvesting skills
- Context compression techniques

What is still missing is a **coherent, install-once orchestration layer** that makes the agent the primary owner of its own low-level tool surface (especially deterministic shell workflows) and that systematically discovers, prefers, and improves that surface.

This project aims to fill that gap, starting as a focused power-user tool (primarily Claude Code) rather than a universal product.

## Core principles (v0)

- **Local first** — always prefer existing project/user skills, scripts, and aliases
- **Deterministic when possible** — turn recurring multi-step shell sequences into short named scripts/aliases
- **Conservative discovery** — external install is opt-in or gated; never silent free-for-all
- **Reflection is explicit** — create/improve only when a clear recurring pattern succeeded
- **Token hygiene** — the orchestration itself must stay lightweight
- **Scope discipline** — start narrow (Claude Code + local + curated registries), expand later

## Repository layout

```
docs/
  VISION.md          # Product vision and goals
  SPEC.md            # High-level specification
  PROBLEMS.md        # Hard problems and how we plan to tackle them
  ARCHITECTURE.md    # Shape of the system (evolving)
  ROADMAP.md         # Phased plan (to be written)
```

## Current focus

We are still shaping the design. See the docs above. Implementation will begin once the problem-tackling strategies and core interfaces are clear enough.

## License

TBD (likely MIT or Apache-2.0).
