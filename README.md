# aha-orch

Capability orchestration framework skill package for AI agents.

## What is aha-orch

aha-orch is a runtime-neutral framework that defines how an AI agent detects available capability surfaces, converges them into an execution route, executes with transparency, and re-orchestrates when a capability gap appears.

It is a decision contract, not an SOP. Agents apply the framework across native runtime capability, enhancement layers, skills, MCP surfaces, commands, and subagent/worktree collaboration patterns.

## Three Skill Packages

| Skill | Purpose | Runtime |
|---|---|---|
| `aha-orch-xx` | Runtime-agnostic complete skill | Any |
| `aha-codex-omx` | Codex + OMX optimized | Codex with oh-my-codex |
| `aha-opencode-omo` | OpenCode + OMO optimized | OpenCode with oh-my-opencode |

Each skill package contains the shared framework document (`capability-orchestration.md`) plus runtime-specific implementation guidance.

## Installation

Copy the desired skill directory into your runtime's skills path:

- **Codex**: copy `aha-codex-omx/` to your Codex skills directory.
- **OpenCode**: copy `aha-opencode-omo/` to your OpenCode skills directory.
- **Other runtimes**: copy `aha-orch-xx/` to the appropriate skills path.

## Framework Document

See `capability-orchestration.md` in any skill directory for the full framework.

## License

MIT-0. See `LICENSE`.
