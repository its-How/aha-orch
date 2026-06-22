---
name: aha-codex-omx
description: "Codex+OMX optimized capability orchestration skill. Use this when in Codex with OMX installed. Activates full delegation mode with OMX-specific capability discovery and task-driven orchestration."
---

# aha-codex-omx

## What This Mode Activates

Full-delegation capability orchestration for [Codex CLI](https://github.com/openai/codex) with [oh-my-codex (OMX)](https://github.com/Yeachan-Heo/oh-my-codex) installed. This skill enables the agent to autonomously discover, select, combine, and reselect available capability surfaces (native runtime, enhancement layer, skill, MCP, command, subagent, worktree) to build the lowest-sufficient execution route for each task unit.

## Pre-Check

1. Verify OMX is installed: `omx --version`
2. Confirm runtime family: Codex (not [OpenCode](https://github.com/sst/opencode), not [oh-my-openagent (OMO)](https://github.com/code-yeongyu/oh-my-openagent))
3. **Wrong-runtime guard**: If you are in OpenCode with OMO, use `aha-opencode-omo` instead. This skill is for Codex+OMX only.
4. If OMX is not detected, proceed with native Codex capabilities and state the limitation transparently.

## Capability Discovery

Run discovery on every orchestration pass. Capability surfaces change across sessions, projects, versions, and permission modes.

1. **Primary tools**: `omx list` to enumerate installed skills and enhancement layers; `explore` for codebase exploration; `autoresearch` for iterative research
2. **Secondary scan**: check for configured MCPs, available commands, validators, and native subagent surfaces
3. **Permission envelope**: determine read-only vs write, external-write, network, approval policy, and destructive-action limits

See `./capability-orchestration.md` for the 7-field discovery schema.

If discovery fails, transparently tell the user, fall back to built-in reference knowledge, mark it as possibly outdated, and invite the user to provide current capability information. Do not overclaim actual availability.

## Do NOT Use This Mode For

- Trivial single-step edits or read-only Q&A where native Codex is sufficient
- Tasks that require explicit human confirmation at every step
- Environments where OMX is not installed and cannot be installed

## Rollback / Deactivation

To deactivate: stop using OMX-specific capabilities and fall back to native Codex. No persistent state is maintained by this skill.

## Reference

- Read `./capability-orchestration.md` before applying orchestration logic. It is the source of truth for orchestration steps, transparency, re-orchestration, out-of-session, cost awareness, and the 7-field discovery schema.
