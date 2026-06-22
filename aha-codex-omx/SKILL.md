---
name: aha-codex-omx
description: "Codex+OMX optimized capability orchestration skill. Use this when in Codex with OMX installed. Activates full delegation mode with OMX-specific capability discovery and task-driven orchestration."
---

# aha-codex-omx

## What This Mode Activates

Full-delegation capability orchestration for Codex with OMX installed. This skill enables the agent to autonomously discover, select, combine, and reselect available capability surfaces (native runtime, enhancement layer, skill, MCP, command, subagent, worktree) to build the lowest-sufficient execution route for each task unit.

## Pre-Check

1. Verify OMX is installed: `omx --version`
2. Confirm runtime family: Codex (not OpenCode, not OMO)
3. **Wrong-runtime guard**: If you are in OpenCode with OMO, use `aha-opencode-omo` instead. This skill is for Codex+OMX only.
4. If OMX is not detected, proceed with native Codex capabilities and state the limitation transparently.

## Capability Discovery

Run discovery on every orchestration pass. Capability surfaces change across sessions, projects, versions, and permission modes.

1. **Primary tools**: `omx list` to enumerate installed skills and enhancement layers; `explore` for codebase exploration; `autoresearch` for iterative research
2. **Secondary scan**: check for configured MCPs, available commands, validators, and native subagent surfaces
3. **Permission envelope**: determine read-only vs write, external-write, network, approval policy, and destructive-action limits

Each discovered capability must include:
- Type (skill / MCP / command / validator / subagent / native / other)
- Name
- Category (planning / exploration / implementation / review / verification / browser / external API / context / handoff / rollback / utility)
- Status (available / unavailable / configured / detected / uncertain / failed / disabled / requires confirmation)
- Description
- Trigger conditions (when to use and when to avoid)
- Risk level (low / medium / high)

If discovery fails, transparently tell the user, fall back to built-in reference knowledge, mark it as possibly outdated, and invite the user to provide current capability information. Do not overclaim actual availability.

## Capability Orchestration

Build the execution route from the discovered capability surface and task shape. Reference `./capability-orchestration.md` for the full framework.

- Judge complexity from the highest granularity downward, then converge to the lowest sufficient route
- Use the tier table as a coordinate reference, not as user-facing status text
- Mix capabilities across surfaces when mixed orchestration is lower-risk or more complete than a single surface
- Trigger secondary confirmation for: large subagent fan-out, worktree usage, cross-domain integration, and high execution cost

## Orchestration Transparency

Keep the full chain transparent: initial orchestration, execution-relevant capability choices, gap-triggered re-orchestration, and Out-of-Session recommendations.

Disclose to the user before meaningful execution when the route materially changes collaboration shape, risk, cost, or confirmation needs. Provide capability-use guidance; do not expose tier names as the explanation.

## Re-orchestration on Gap

When execution reveals a capability gap, constraint conflict, failed validation, unavailable surface, context overload, or permission mismatch, re-orchestrate instead of silently degrading.

Transparently tell the user what changed and why, but do not announce tier names as the explanation.

## Out-of-Session

Recommend Out-of-Session when the current session is a poor container: polluted context, different permission scope needed, different project boundary required, or a handoff artifact is needed before continuation.

Create a handoff file with: Reason, Complete Prompt, Task Background, Suggested Runtime / Enhancement Layer, Related File Paths, and Context Summary. Do not include credentials, tokens, cookies, session material, provider state, live state, or account state in handoff material.

## Do NOT Use This Mode For

- Trivial single-step edits or read-only Q&A where native Codex is sufficient
- Tasks that require explicit human confirmation at every step
- Environments where OMX is not installed and cannot be installed

## Cost Awareness

- Prefer the lowest sufficient capability surface for each unit
- Avoid large subagent fan-out for tasks that do not benefit from parallel execution
- Do not treat capability activation as success; verify task outcome evidence

## Rollback / Deactivation

To deactivate: stop using OMX-specific capabilities and fall back to native Codex. No persistent state is maintained by this skill.

## Reference

- `./capability-orchestration.md` — full capability orchestration framework
