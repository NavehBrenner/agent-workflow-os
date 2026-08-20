# Vision

## One-sentence goal

After a single install into a repository, the coding agent becomes largely self-managing with respect to its own workflows: it prefers existing local capabilities, discovers and installs missing ones when useful, uses helpers efficiently, and continuously improves its deterministic tool surface (skills, scripts, aliases).

## The user experience we want

When creating a new project the human does roughly:

1. `install agent-workflow-os` (one command)
2. `install code-quality-harness` (separate project the author is also working on)
3. Start the agent and work.

From that point the human should not have to constantly:

- re-teach the same multi-step shell sequences
- hunt for the right skill
- decide whether to create a new alias or skill
- fight context bloat from repeated long command chains

The agent should carry that burden.

## What "works well" means for us

For the author's own projects and a small set of similar users:

- Recurring deterministic shell sequences become short named scripts/aliases that the agent prefers
- Local skills are checked first and used when relevant
- External skills can be discovered and installed with clear safety gates
- Reflection happens after successful workflows and produces useful local improvements
- The system itself does not become a new source of significant token or maintenance cost
- The human still feels in control (especially around external installs and destructive operations)

We are **not** initially aiming for a fully autonomous, zero-babysitting experience for every possible user and every agent. That is a later aspiration.

## Scope boundaries (v0 / v1)

**In scope**

- Claude Code as primary target
- Local skills + project/user scripts + shell/git aliases
- A small number of curated external registries
- Explicit reflection and local creation of deterministic helpers
- Clear standing policy the agent is instructed to follow

**Out of scope for early versions**

- Perfect cross-agent support
- Fully automatic unattended external installs from arbitrary sources
- Replacing high-level planning or domain reasoning
- Competing with general agent frameworks or full harnesses

## Relationship to existing building blocks

We deliberately sit *on top of* existing primitives rather than replacing them:

- Skills / SKILL.md ecosystem
- Claude Code plugins and marketplaces
- Shell and git aliases
- CLI wrapper scripts as agent tools
- Self-learning / harvesting skill patterns
- Existing install CLIs (`npx skills`, PolySkill, etc.)

The value is the **orchestration + preference + reflection + local deterministic surface** layer that currently has to be assembled by hand.
