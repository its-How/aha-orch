---
name: aha-orch-xx
description: "Runtime-agnostic capability orchestration skill. Activates full delegation mode with capability discovery and task-driven orchestration. Use this to maximize runtime + enhancement layer capabilities. If you have a runtime-specific skill (aha-codex-omx / aha-opencode-omo), prefer that instead."
---

# What This Skill Activates

This skill is a runtime-neutral orchestration framework. It does not prescribe concrete tools, commands, or runtime implementations. Instead, it tells the agent how to detect the current execution context, discover all available capability surfaces, converge them into the lowest sufficient execution route, execute with transparency, and re-orchestrate when a capability gap appears.

Use this skill when no runtime-specific skill is available. If aha-codex-omx or aha-opencode-omo is present and matches the active runtime, prefer that instead.

# Do NOT Use This Skill For

- Tasks that are already covered by a runtime-specific skill (aha-codex-omx / aha-opencode-omo).
- Situations where the user explicitly wants a fixed, non-adaptive execution route.
- Bypassing confirmation-gated actions, permission limits, or safety boundaries.
- Claiming capability availability without evidence.

# Rollback / Deactivation

To deactivate this skill, stop applying the orchestration framework. If the runtime-specific skill is available, switch to it. If neither is appropriate, fall back to the runtime's default behavior. There is no persistent state to clean up.

# Reference

- Read `./capability-orchestration.md` before applying orchestration logic. It is the source of truth for runtime detection, capability discovery fields, orchestration, transparency, re-orchestration, out-of-session, and cost awareness.
- If aha-codex-omx or aha-opencode-omo is available and matches the active runtime, prefer that runtime-specific skill instead.
