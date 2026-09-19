<div align="center">

# processon-skills

**ProcessOn AIGC skills — flowcharts, swimlanes, UML, architecture & ER diagrams, mind maps, structured infographics, generation prompts, and review contracts**

[![GitHub](https://img.shields.io/badge/github-full--stack--skills%2Fprocesson--skills-green.svg)](https://github.com/full-stack-skills/processon-skills)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-purple.svg)](https://agentskills.io)

English | [简体中文](./README.zh-CN.md)

</div>

---

## 📖 Overview

**processon-skills** is a set of AI coding-agent skills in the [Full Stack Skills](https://github.com/full-stack-skills) ecosystem, with **7 skills** covering the full ProcessOn diagramming workflow — classify → model → prompt → generate → review → deliver — producing **editable** diagrams through the official ProcessOn MCP server.

## 📦 Installation

```bash
npx skills add full-stack-skills/processon-skills
```

## 🎯 Skills (7)

| Skill | Description |
|------|------|
| `processon-use` | Router: dispatches ProcessOn drawing requests to the smallest applicable workflow (diagram / mindmap / infographic) |
| `processon-diagram` | Model flowcharts, swimlanes, UML, sequence, architecture, ER, org charts, timelines, and business analysis frameworks |
| `processon-mindmap` | Turn text, documents, plans, and knowledge into mind maps, logic maps, org maps, fishbones, timelines, and WBS trees |
| `processon-infographic` | Map comparison, cycle, matrix, progression, hierarchy, and radial relationships to report-ready infographic layouts |
| `processon-prompt` | Convert an approved diagram structure into a precise ProcessOn generation prompt with layout and visual constraints |
| `processon-review` | Post-generation review of semantic correctness, visual hierarchy, readability, layout fit, consistency, and editability (bounded REVISE_ONCE) |
| `processon-setup` | Three-step local ProcessOn Token setup, invalid-credential recovery, and safe rotation (credentials never enter chat, files, or logs) |

## 🤖 Supported Agents

Works with [Claude Code](https://code.claude.com), [Codex](https://developers.openai.com/codex), [Cursor](https://cursor.com), [OpenCode](https://opencode.ai), [Gemini CLI](https://geminicli.com), [GitHub Copilot](https://github.com/features/copilot), [Windsurf](https://codeium.com/windsurf), and [70+ others](https://agentskills.io/clients).

### Claude Code Installation

**Option 1: npx skills CLI (recommended)**

```bash
npx skills add full-stack-skills/processon-skills
```

**Option 2: manual**

```bash
git clone https://github.com/full-stack-skills/processon-skills.git
cp -r processon-skills/skills/* .claude/skills/
```

## 🔌 Host Integrations

The skills are host-agnostic. Known consumers:

- [codex-processon-plugin](https://github.com/partme-ai/codex-processon-plugin) (Codex plugin; vendors this package via `skills.lock.json`)
- The WorkBuddy ProcessOn team ([workbuddy-agent-experts](https://github.com/partme-ai/workbuddy-agent-experts), vendored at build time)

<!-- FULL_STACK_DOC_START -->
## Project positioning and boundaries

`processon-skills` is the source repository for **7 independently installable Agent Skills**. The package manifest currently reports version `1.0.1`. This repository owns trigger contracts, workflows, references, examples, and quality gates; executable hooks, MCP servers, credential injection, and provider runtimes belong to consuming plugins.

| Confirmed fact | Value | Evidence |
|---|---|---|
| Package | `full-stack-skills/processon-skills` | `.claude-plugin/plugin.json`, repository remote |
| Installable skills | 7 | `skills/*/SKILL.md` |
| Current version | `1.0.1` | `.claude-plugin/plugin.json` |
| Specification source | OpenSpec | `openspec/config.yaml` |
| License | Apache-2.0 | `LICENSE` |

### Out of scope

- This package does not replace executable harnesses, MCP services, hooks, or provider clients.
- Copying `SKILL.md` does not prove host discovery, triggering, or successful execution.
- Skills do not silently authorize network calls, paid generation, overwrites, uploads, or publishing.
- Managed copies inside consumer plugins must be updated from immutable releases, not edited directly.

## At a glance

```text
user task -> name/description discovery -> read SKILL.md
          -> load only required references/examples/scripts
          -> execute domain workflow -> collect evidence
          -> PASS / FAIL / UNVERIFIED
```

## Verified installation and discovery

```bash
npx skills add full-stack-skills/processon-skills
npx skills add full-stack-skills/processon-skills --skill processon-diagram
npx skills list --json
```

Use an immutable GitHub Release/tag when pinning a version; do not treat a moving `main` branch as a release. After installation, verify the skill count, names, resources, and target-agent list. Real Codex, ZCode, and Kimi plugin loading remains a separate runtime proof level.

## Package structure and loading

```text
processon-skills/
├── .claude-plugin/plugin.json
├── skills/<name>/SKILL.md
├── skills/<name>/references/
├── skills/<name>/examples/
├── scripts/
├── openspec/
└── LICENSE
```

Cross-skill handoffs must use the skill name and install command, never a `../sibling-skill/` link: granular installations may contain only one skill.

## Quality, release, and security

```bash
python3 scripts/lint_skills.py
```

Before release, verify frontmatter, relative links, bundled resources, TRACE thresholds, manifest versions, and a clean-environment install. Published tags are immutable. A consuming plugin upgrades through a reviewed lock change containing the release tag, peeled SHA, and content digests.

Do not commit credentials, accounts, local absolute paths, or private repository names. Paid, upload, delete, overwrite, and publish operations require explicit authorization.

## Troubleshooting

| Symptom | Check | Resolution |
|---|---|---|
| Skill is not discovered | Frontmatter, agent discovery path, refresh requirement | Confirm with `skills list --json` |
| Granular install has missing references | Cross-skill relative paths | Move required resources into the skill or install the dependency by name |
| Plugin integrity check fails | Tag, peeled SHA, digest, local-skill manifest | Publish a new source release and update through the sync PR |
| Tool or credential is unavailable | `compatibility` and runtime prerequisites | Report `UNVERIFIED`; do not claim success |
| A second generator run changes files | Non-idempotent generation or manifest drift | Block release and repair generation/sorting |
<!-- FULL_STACK_DOC_END -->

## 📄 License

Apache 2.0
