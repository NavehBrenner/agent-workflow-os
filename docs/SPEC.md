# High-level Specification (v0)

This document captures the intended behavior of agent-workflow-os at a product level. It is still evolving.

## 1. Installation contract

A single command (exact form TBD) run inside a repository should:

- Install the core policy / skill(s) that define the standing behavior
- Create or ensure the local directories for project-scoped scripts, aliases, and generated skills
- Optionally register a small set of trusted registries or discovery helpers
- Leave behind clear documentation the agent can read about the preferred workflow loop

After install, the human should not need to perform further setup for the basic loop to function.

## 2. Standing policy the agent is expected to follow

When faced with a new task the agent should, in roughly this order:

1. **Local capability check**  
   Look for an existing local skill, script, or alias that already does (or nearly does) what is needed. Prefer it.

2. **External discovery (gated)**  
   If nothing local is adequate, consider whether a known registry contains a relevant skill. Propose or (if policy allows) install it. Do not perform open-ended internet searches for skills by default.

3. **Efficient execution**  
   Use helpers, subagents, and short deterministic scripts where they reduce context and error surface. Avoid re-planning long deterministic shell sequences from scratch.

4. **Reflection & local improvement**  
   After a successful multi-step workflow that looks recurring and deterministic, consider creating or improving a local script/alias/skill so the next occurrence is cheaper and more reliable.

This policy is expressed primarily as instructions the agent loads (skill, CLAUDE.md fragment, or equivalent), not as a hard runtime enforcer in v0.

## 3. Local surface the system owns

The system should maintain and prefer a small, well-known local surface:

- Project scripts directory (e.g. `bin/` or `.agent/scripts/`)
- Shell or git aliases that are project- or user-scoped and discoverable
- Local skills (project-scoped under `.claude/skills/` or equivalent)
- A lightweight manifest or index of what has been created so the agent can list them cheaply

Deterministic multi-step shell sequences (example: stash → switch to main → pull → switch back → pop) are first-class candidates for promotion into short named scripts/aliases.

## 4. External discovery model

- Start with a **curated allowlist** of registries / marketplaces
- Discovery is triggered by the agent under the standing policy, not by continuous background scanning
- Install actions are **conservative**: propose + confirm by default; auto-install only from explicitly trusted sources or under an explicit user flag
- Installed external skills are recorded so they can be audited and pruned later

## 5. Reflection model

Reflection is not continuous free-form self-modification. It is a deliberate step:

- Triggered after successful completion of a workflow that involved multiple shell steps or a clear recurring pattern
- Candidate outcomes: new script/alias, improved existing script, new or updated local skill
- The agent should explain what it is creating and why (at least in the session)
- Safety: generated scripts should prefer non-destructive defaults; destructive operations remain gated

## 6. Non-goals for early versions

- Replacing the agent's general reasoning or planning
- Guaranteeing perfect compliance with the standing policy
- Supporting every coding agent equally from day one
- Fully automatic unattended installation from arbitrary public sources
- Solving all context-window problems (we only target the repetitive deterministic portion)

## 7. Success criteria (early)

For the author's own repositories:

- Recurring shell sequences are observably turned into short names that the agent reuses
- The agent checks local capabilities before inventing long command chains
- External installs only happen with clear visibility and control
- The overhead of the orchestration layer itself stays small
- The human feels less need to manually curate the same workflows repeatedly
