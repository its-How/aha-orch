# aha-orch

Capability orchestration framework skill package for AI agents.

## What is aha-orch

aha-orch is a runtime-neutral framework that defines how an AI agent detects available capability surfaces, converges them into an execution route, executes with transparency, and re-orchestrates when a capability gap appears.

It is a decision contract, not an SOP. Agents apply the framework across native runtime capability, enhancement layers, skills, MCP surfaces, commands, and subagent/worktree collaboration patterns.

## Four Skill Packages

| Skill | Purpose | Runtime |
|---|---|---|
| `aha-orch-xx` | Runtime-agnostic complete skill | Any |
| `aha-codex-omx` | [Codex CLI](https://github.com/openai/codex) + [oh-my-codex (OMX)](https://github.com/Yeachan-Heo/oh-my-codex) optimized | Codex with oh-my-codex |
| `aha-opencode-omo` | [OpenCode](https://github.com/sst/opencode) + [oh-my-openagent (OMO)](https://github.com/code-yeongyu/oh-my-openagent) optimized | OpenCode with oh-my-openagent |
| `aha-claudecode-omc` | [Claude Code](https://github.com/anthropics/claude-code) + [oh-my-claudecode (OMC)](https://github.com/Yeachan-Heo/oh-my-claudecode) optimized | Claude Code with oh-my-claudecode |

Each skill package contains the shared framework document (`capability-orchestration.md`) plus runtime-specific implementation guidance.

## Installation

### Option 1: skills.sh

```bash
# Install all 4 skills
npx skills add its-how/aha-orch

# Or install a specific skill
npx skills add its-how/aha-orch --skill aha-codex-omx
npx skills add its-how/aha-orch --skill aha-opencode-omo
npx skills add its-how/aha-orch --skill aha-orch-xx
npx skills add its-how/aha-orch --skill aha-claudecode-omc
```

### Option 2: ClawHub

```bash
clawhub install aha-codex-omx
clawhub install aha-opencode-omo
clawhub install aha-orch-xx
clawhub install aha-claudecode-omc
```

### Option 3: Manual copy

Copy the desired skill directory into your runtime's skills path:

- **Codex**: copy `aha-codex-omx/` to `~/.codex/skills/` or `.agents/skills/`
- **OpenCode**: copy `aha-opencode-omo/` to `~/.config/opencode/skills/` or `.agents/skills/`
- **Claude Code**: copy `aha-claudecode-omc/` to `~/.claude/skills/` or `.agents/skills/`
- **Other runtimes**: copy `aha-orch-xx/` to the appropriate skills path for your runtime

## Framework Document

See `capability-orchestration.md` in any skill directory for the full framework.

## License

MIT-0. See `LICENSE`.
