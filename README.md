# crossmodel-review

A [Claude Code skill](https://docs.anthropic.com/en/docs/claude-code/skills) that gets you a second opinion on your work by sending it to frontier models from Google and OpenAI via GitHub Copilot CLI, then synthesizing the results.

Inspired by the [PAL MCP Server](https://github.com/BeehiveInnovations/pal-mcp-server) clink pattern, but focused on doing one thing well: cross-model code review.

## How it works

1. Discovers available models from your Copilot CLI
2. Recommends the latest frontier models (Google + OpenAI) and lets you pick
3. Sends your artifact to both models in parallel with a role-appropriate review prompt
4. Synthesizes the results — highlighting agreements, flagging disagreements, and listing actionable next steps

Works with code, PRDs, architecture docs, or any artifact that benefits from a critical review.

## Prerequisites

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) installed
- [GitHub Copilot CLI](https://www.npmjs.com/package/@github/copilot) installed and authenticated:
  ```bash
  npm install -g @github/copilot
  copilot        # then use /login to authenticate
  ```

## Install

### Per-project (shared with your team via version control)

Copy the `crossmodel-review` directory into your project's `.claude/skills/`:

```bash
# From your project root
mkdir -p .claude/skills
cp -r /path/to/crossmodel-review .claude/skills/crossmodel-review
```

Or add it as a git submodule:

```bash
git submodule add https://github.com/<your-username>/crossmodel-review .claude/skills/crossmodel-review
```

### Personal (available across all your projects)

```bash
cp -r /path/to/crossmodel-review ~/.claude/skills/crossmodel-review
```

## Usage

In Claude Code, run:

```
/crossmodel-review path/to/file.py
```

Claude will:
- Verify Copilot CLI is ready
- Discover available models and ask you to confirm the picks
- Auto-detect whether it's code, a PRD, or an architecture doc
- Run parallel reviews and synthesize the feedback

## Permissions

The skill requires Bash access to invoke the Copilot CLI. When Claude Code prompts you, allow Bash execution for `copilot` commands.

## License

MIT
