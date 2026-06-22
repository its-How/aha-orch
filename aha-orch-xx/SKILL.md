---
name: aha-orch-xx
description: "Runtime-agnostic capability orchestration skill. Activates full delegation mode with capability discovery and task-driven orchestration. Use this to maximize runtime + enhancement layer capabilities. If you have a runtime-specific skill (aha-codex-omx / aha-opencode-omo), prefer that instead."
---

# What This Skill Activates

This skill is a runtime-neutral orchestration framework. It does not prescribe concrete tools, commands, or runtime implementations. Instead, it tells the agent how to detect the current execution context, discover all available capability surfaces, converge them into the lowest sufficient execution route, execute with transparency, and re-orchestrate when a capability gap appears.

Use this skill when no runtime-specific skill is available. If aha-codex-omx or aha-opencode-omo is present and matches the active runtime, prefer that instead.

# Pre-Check: Runtime Detection

Before planning capability use, detect the active execution context: runtime family and invocation mode; active enhancement layer, if any; runtime version and enhancement version when version-sensitive behavior affects capability availability; current permission envelope (read-only, workspace-write, external-write, network availability, approval policy, destructive-action limits); available collaboration surfaces (native subagent, configured subagent, skill, command, MCP, plugin, worktree, background task, validator, shell, browser, or equivalent runtime-neutral capability class); and explicit user invocation signals that change orchestration expectations. If detection fails, proceed with the safest native capability assumption, state the uncertainty, and avoid claiming unavailable surfaces.

# Capability Discovery

Pull the full capability surface for the current runtime context on every orchestration pass. Discovery must include native capability plus any active enhancement layer, skill, MCP, command, validator, and collaboration surfaces available to the session.

Each discovered capability record must include at minimum:

1. **Type** — Capability class: native, enhancement layer, skill, MCP, command, validator, subagent, worktree, browser, or equivalent.
2. **Name** — Stable capability name as exposed by the runtime or enhancement surface.
3. **Category** — Primary use class: planning, exploration, implementation, review, verification, browser, external API, context, handoff, rollback, or equivalent.
4. **Status** — Available, unavailable, configured, detected, uncertain, failed, disabled, or requires confirmation.
5. **Description** — Short operational description of what the capability can do.
6. **Trigger Conditions** — When to consider using it and when to avoid it.
7. **Risk Level** — Low, medium, or high, based on permission surface, external side effects, credential/provider/browser/live exposure, state mutation, cost, and reversibility.

Run discovery every time because capability surfaces can change across sessions, projects, runtime versions, permission modes, and enhancement activation states. If discovery fails, transparently tell the user that live capability discovery failed, may use built-in reference knowledge as a fallback, mark it as possibly outdated, and invite the user to provide current capability information. Do not overclaim actual availability.

# Capability Orchestration

Build an orchestration plan from the discovered capability surface and task shape.

Determine: goal decomposition (smallest complete units, dependency order, validation gates); capability convergence (which surfaces are sufficient, redundant, risky, unavailable, or better held in reserve); orchestration granularity (single-agent, few subagents, multiple subagents, large fan-out, worktree-backed lanes, or external handoff); collaboration complexity (simple serial work, planned serial work, simple parallel work, autonomous loops, persistent execution, cross-domain integration, or high-cost parallel integration); confirmation triggers (whether orchestration features require secondary confirmation before execution); and transparency payload (what capability route will be used, what is intentionally not used, and what the user can request if they want a different capability route). Judge orchestration complexity from the highest complexity downward, then converge to the lowest sufficient route. The tier table is a coordinate reference, not a user-facing label. See `./capability-orchestration.md` for the full framework. Mix capabilities across native runtime, enhancement layer, skill, MCP, command, subagent, and worktree surfaces when mixed orchestration is lower-risk or more complete than choosing a single surface.

# Orchestration Transparency

Keep the full orchestration chain transparent across initial orchestration and re-orchestration. Tell the user: which capability classes will be used; which tempting capability classes are skipped and why; what the user can request if they want more parallelism, less autonomy, a different runtime container, or stricter verification; what requires secondary confirmation and which orchestration features triggered it; and how execution success will be verified. Do not use tier names as the primary user-facing explanation. Say what will happen, not the coordinate label.

# Re-orchestration on Gap

When execution reveals a capability gap, constraint conflict, failed validation, unavailable surface, context overload, or permission mismatch, re-orchestrate instead of silently degrading. Answer: which route failed or became insufficient; which gap class appeared (missing capability, unsafe capability, failed capability, stale discovery, permission limit, context limit, validation failure, or cross-domain mismatch); which route is next (converge downward, mix capabilities, select a different capability class, request secondary confirmation, or recommend Out-of-Session); how the new route will be orchestrated; whether capability mixing or single-route selection is safer and why; and what the user needs to know (changed capability route, changed risk/cost, changed validation path, and any capability-use instruction). Be transparent. Tell the user what changed and why, but do not announce tier names as the explanation.

# Out-of-Session

Recommend Out-of-Session when the current session is a poor execution container: clean context is materially better, different permission scope is needed, different project boundary is required, or a handoff artifact is needed before another container continues.

When recommending Out-of-Session, create or request permission to create a handoff file with these fields: Reason, Complete Prompt, Task Background, Suggested Runtime / Enhancement Layer, Related File Paths, and Context Summary. Place the handoff file in a workspace temporary directory, `~/tmp/`, or `/tmp/`. In a read-only environment, request write permission; if denied, output the handoff content inline.

Out-of-Session material must not include credentials, tokens, cookies, browser session material, provider state, live state, account state, or equivalent secrets.

# Do NOT Use This Skill For

- Tasks that are already covered by a runtime-specific skill (aha-codex-omx / aha-opencode-omo).
- Situations where the user explicitly wants a fixed, non-adaptive execution route.
- Bypassing confirmation-gated actions, permission limits, or safety boundaries.
- Claiming capability availability without evidence.

# Cost Awareness

Orchestration complexity carries cost. Prefer the lowest sufficient route. Avoid large fan-out when few subagents suffice. Avoid worktree-backed lanes when simple serial work is enough. Avoid persistent loops when a single pass completes the task. Re-orchestrate on gap, but do not re-plan for every tool call.

# Rollback / Deactivation

To deactivate this skill, stop applying the orchestration framework. If the runtime-specific skill is available, switch to it. If neither is appropriate, fall back to the runtime's default behavior. There is no persistent state to clean up.

# Reference

- `./capability-orchestration.md` — Full runtime-neutral orchestration framework source.
- If aha-codex-omx or aha-opencode-omo is available and matches the active runtime, prefer that runtime-specific skill instead.