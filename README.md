<div align="center">

# processon-skills

**ProcessOn AIGC skills — flowcharts, swimlanes, UML, architecture & ER diagrams, mind maps, structured infographics, generation prompts, and review contracts**

[![GitHub](https://img.shields.io/badge/github-full--aigc--skills%2Fprocesson--skills-green.svg)](https://github.com/full-aigc-skills/processon-skills)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-compatible-purple.svg)](https://agentskills.io)

English | [简体中文](./README.zh-CN.md)

</div>

---

## 📖 Overview

**processon-skills** is a set of AI coding-agent skills in the [Full AIGC Skills](https://github.com/full-aigc-skills) ecosystem, with **7 skills** covering the full ProcessOn diagramming workflow — classify → model → prompt → generate → review → deliver — producing **editable** diagrams through the official ProcessOn MCP server.

## 📦 Installation

```bash
npx skills add full-aigc-skills/processon-skills
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
npx skills add full-aigc-skills/processon-skills
```

**Option 2: manual**

```bash
git clone https://github.com/full-aigc-skills/processon-skills.git
cp -r processon-skills/skills/* .claude/skills/
```

## 🔌 Host Integrations

The skills are host-agnostic. Known consumers:

- [codex-processon-plugin](https://github.com/partme-ai/codex-processon-plugin) (Codex plugin; vendors this package via `skills.lock.json`)
- The WorkBuddy ProcessOn team ([workbuddy-agent-experts](https://github.com/partme-ai/workbuddy-agent-experts), vendored at build time)

## 📄 License

Apache 2.0
