---
name: aha-opencode-omo
description: "OpenCode+OMO optimized capability orchestration skill. Use this when in OpenCode with OMO installed. Activates full delegation mode with OMO-specific capability discovery and task-driven orchestration."
---

# aha-opencode-omo

## What This Mode Activates

Full-delegation capability orchestration for [OpenCode](https://github.com/sst/opencode) with [oh-my-openagent (OMO)](https://github.com/code-yeongyu/oh-my-openagent) installed. This skill enables the agent to autonomously discover, select, combine, and reselect available capability surfaces (native runtime, enhancement layer, skill, MCP, command, subagent, worktree) to build the lowest-sufficient execution route for each task unit.

## Pre-Check

1. Verify OMO is installed: `opencode agent list`
2. Confirm runtime family: OpenCode (not [Codex CLI](https://github.com/openai/codex), not [oh-my-codex (OMX)](https://github.com/Yeachan-Heo/oh-my-codex))
3. **Wrong-runtime guard**: If you are in Codex with OMX, use `aha-codex-omx` instead. This skill is for OpenCode+OMO only.
4. If OMO is not detected, proceed with native OpenCode capabilities and state the limitation transparently.

## Capability Discovery

Run discovery on every orchestration pass. Capability surfaces change across sessions, projects, versions, and permission modes.

1. **Primary tool**: `opencode agent list` to enumerate available agents and enhancement layers
2. **Secondary scan**: use `librarian` to query installed skills, MCPs, commands, validators, and native subagent surfaces
3. **Permission envelope**: determine read-only vs write, external-write, network, approval policy, and destructive-action limits

See `./capability-orchestration.md` for the 7-field discovery schema.

If discovery fails, transparently tell the user, fall back to built-in reference knowledge, mark it as possibly outdated, and invite the user to provide current capability information. Do not overclaim actual availability.

## Do NOT Use This Mode For

- Trivial single-step edits or read-only Q&A where native OpenCode is sufficient
- Tasks that require explicit human confirmation at every step
- Environments where OMO is not installed and cannot be installed

## Rollback / Deactivation

To deactivate: stop using OMO-specific capabilities and fall back to native OpenCode. No persistent state is maintained by this skill.

## Reference

- Read `./capability-orchestration.md` before applying orchestration logic. It is the source of truth for orchestration steps, transparency, re-orchestration, out-of-session, cost awareness, and the 7-field discovery schema.
