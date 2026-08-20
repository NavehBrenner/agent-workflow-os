# Hard Problems and How We Plan to Tackle Them

This document is the living analysis of the main difficulties identified in design discussions. Each problem includes a proposed direction so that implementation has a concrete foundation.

## 1. Agent compliance (ignoring the preferred path)

**Problem**  
Even with clear standing instructions, models sometimes ignore the local-first / short-alias policy and re-invent long command sequences or skip discovery.

**Direction**
- Make the preferred path the *easiest* path: short names, clear descriptions, and a tiny local index the agent can read cheaply.
- Keep the standing policy short, high-signal, and placed where the agent loads it reliably (skill + optional CLAUDE.md fragment).
- Prefer positive framing ("prefer X when available") over long lists of prohibitions.
- Accept that compliance will never be 100%. Design for "usually followed" rather than "enforced".
- Later: optional lightweight hooks or pre-tool checks if the host supports them, but do not depend on them for v0.

## 2. Discovery quality and noise

**Problem**  
Searching external registries can return irrelevant, low-quality, or overlapping skills. Bad installs increase context cost and confusion.

**Direction**
- Curated allowlist of registries only in early versions.
- Discovery is agent-triggered under the standing policy, not continuous.
- Require a clear relevance judgment before proposing install.
- Prefer skills with good descriptions and (when available) usage signals.
- Record every install for later audit and pruning.
- Do not attempt open-web skill search by default.

## 3. Security of auto-install and generated scripts

**Problem**  
Letting an agent install and run code from external sources, or write its own scripts that later execute, is a real risk.

**Direction**
- Default mode: **propose + human confirm** for external installs.
- Auto-install only from an explicit allowlist or under a user-enabled "trusted" flag.
- Generated local scripts should start non-destructive; any destructive steps should be obvious and ideally gated.
- Keep a simple audit log of what was created or installed.
- Document the trust model clearly so users know what they are accepting.

## 4. Hygiene and surface growth

**Problem**  
Skills, aliases, and scripts accumulate. Without pruning the agent becomes less decisive and the surface harder to understand.

**Direction**
- Maintain a lightweight manifest / index of local capabilities.
- Reflection should prefer improving an existing helper over creating a near-duplicate.
- Provide a simple "list / audit / prune" path the agent (or human) can use.
- Later: usage signals or staleness heuristics (optional, not required for v0).

## 5. Token and context cost of the orchestration itself

**Problem**  
If the policy, index, and discovery machinery are heavy, they can consume the very context they were meant to save.

**Direction**
- Keep the always-loaded surface small (gateway / pointer style where possible).
- Load full skill content only when relevant.
- Local index should be cheap to list (names + short descriptions).
- Measure and watch the overhead in real sessions; treat bloat as a first-class bug.

## 6. Measuring whether it is actually helping

**Problem**  
It is easy to add layers that feel sophisticated but do not reduce real work or tokens.

**Direction**
- Define a few simple observable signals for the author's own use:
  - Are recurring shell sequences being shortened?
  - Is the agent reusing local helpers?
  - How often does external discovery actually lead to a useful install?
- Start with manual / qualitative evaluation on real projects before building elaborate metrics.
- Avoid optimizing proxy metrics that do not track human friction.

## 7. Ecosystem and host churn

**Problem**  
Claude Code plugins, skill formats, registry APIs, and agent capabilities change. A tightly coupled design will break.

**Direction**
- Depend on the stable, documented parts of the skill ecosystem (SKILL.md, standard directories) first.
- Treat host-specific features (plugins, hooks) as optional accelerators, not core requirements for the basic loop.
- Keep the core policy and local surface host-agnostic where practical so later agents can be added without a full rewrite.

## 8. Scope creep

**Problem**  
The full vision (perfect discovery + perfect reflection + multi-agent + zero babysitting) is attractive and easy to over-build.

**Direction**
- Explicit phased roadmap (see ROADMAP.md once written).
- v0/v1 success = useful for the author's own repos on Claude Code with local-first + conservative discovery + basic reflection.
- Every new capability should be justified against the core user experience, not against completeness.

---

These directions are the starting foundation for architecture and implementation decisions. They will be refined as design discussion continues.
