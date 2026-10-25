# ios-agent-kit

A skill and two templates that teach Claude Code and Codex to build, test, launch and screenshot iOS apps on a Mac with Xcode. They work on any Mac with Xcode: your own, a CI machine, or a [Macswarm](https://macswarm.com) Pod.

| Path | What it is |
| --- | --- |
| [`skills/ios-build-and-test/SKILL.md`](skills/ios-build-and-test/SKILL.md) | Steps and commands for the agent: find the scheme, pick a Simulator by UDID, build, test with a result bundle, launch, screenshot, report |
| [`templates/AGENTS.md`](templates/AGENTS.md) | Instructions to commit at the root of an iOS repository: scheme, test plan, how to prove a change, how to work next to other agents on one Mac |
| [`templates/CLAUDE.md`](templates/CLAUDE.md) | One line, `@AGENTS.md`, so Claude Code reads the same file as Codex |

## Install

### Claude Code

```text
/plugin marketplace add macswarm/ios-agent-kit
/plugin install ios-agent-kit@macswarm
```

Or copy the skill into a repository:

```bash
mkdir -p .claude/skills
cp -R skills/ios-build-and-test .claude/skills/
```

### Codex

Codex loads skills from `.agents/skills` in the repository, or from `~/.agents/skills` for every repository ([Codex docs](https://developers.openai.com/codex/build-skills)).

```bash
mkdir -p .agents/skills
cp -R skills/ios-build-and-test .agents/skills/
```

### Templates

```bash
cp templates/AGENTS.md templates/CLAUDE.md /path/to/your-ios-repo/
```

Fill in the brackets in `AGENTS.md` and commit both files.

## What the skill expects

- macOS with Xcode and at least one iOS Simulator runtime.
- A repository with an `.xcworkspace`, an `.xcodeproj` or a `Package.swift`.
- Optional: an XcodeBuildMCP server. If one is connected the agent may use its tools; the evidence it reports is the same.

The skill never installs Xcode, changes signing or erases Simulators. It writes derived data, result bundles and screenshots under `.build/`.

## Running it on Macswarm

Macswarm Pods come with the Latest Xcode, iOS runtimes, pre-booted Simulators, XcodeBuildMCP, Claude Code and Codex, and run 2 to 3 agents at once in separate git worktrees. See the quickstarts for [Claude Code](https://macswarm.com/docs/quickstart-claude-code/) and [Codex](https://macswarm.com/docs/quickstart-codex/). The Free plan has 3 Pod-hours.

## Contributing

Issues and pull requests are welcome. Keep commands to what ships with Xcode, and test any change on a Simulator before you open the PR.

## License

[MIT](LICENSE)

Mac, macOS, Xcode, and iOS Simulator are trademarks of Apple Inc. Macswarm is not affiliated with or endorsed by Apple. Claude and Claude Code are trademarks of Anthropic; Codex is a trademark of OpenAI.
