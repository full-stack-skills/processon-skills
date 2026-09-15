<div align="center">

# processon-skills

**ProcessOn AIGC 技能 — 流程图、泳道图、UML、架构图、ER 图、思维导图、结构化信息图、生成提示词与审阅契约**

[![GitHub](https://img.shields.io/badge/github-full--aigc--skills%2Fprocesson--skills-green.svg)](https://github.com/full-aigc-skills/processon-skills)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-兼容-purple.svg)](https://agentskills.io)

[English](./README.md) | 简体中文

</div>

---

## 📖 简介

**processon-skills** 是一组 AI 编码智能体技能，属于 [Full AIGC Skills](https://github.com/full-aigc-skills) 生态。包含 **7 个技能**，覆盖"分类 → 建模 → 提示词 → 生成 → 审阅 → 交付"的完整 ProcessOn 制图工作流，经官方 ProcessOn MCP 产出**可编辑**的图形结果。

## 📦 安装

```bash
npx skills add full-aigc-skills/processon-skills
```

## 🎯 技能列表 (7)

| 技能 | 描述 |
|------|------|
| `processon-use` | 路由器：把 ProcessOn 制图请求分发到最窄可用工作流（diagram / mindmap / infographic） |
| `processon-diagram` | 流程图、泳道图、UML、时序图、架构图、ER 图、组织架构、时间线、商业分析框架建模 |
| `processon-mindmap` | 把文本、文档、计划、知识整理为思维导图 / 逻辑图 / 组织图 / 鱼骨图 / 时间线 / WBS 树 |
| `processon-infographic` | 对比、循环、矩阵、递进、层级、辐射关系映射为报告级信息图布局 |
| `processon-prompt` | 把已批准的图形结构转成带布局与视觉约束的 ProcessOn 生成提示词 |
| `processon-review` | 生成后审阅：语义正确性、视觉层级、可读性、布局适配、一致性、可编辑性（REVISE_ONCE 有界返修） |
| `processon-setup` | 本地 ProcessOn Token 的三步配置、失效恢复与安全轮换（凭证永不入对话/文件/日志） |

## 🤖 支持的智能体

适用于 [Claude Code](https://code.claude.com)、[Codex](https://developers.openai.com/codex)、[Cursor](https://cursor.com)、[OpenCode](https://opencode.ai)、[Gemini CLI](https://geminicli.com)、[GitHub Copilot](https://github.com/features/copilot)、[Windsurf](https://codeium.com/windsurf) 及 [70+ 其他](https://agentskills.io/clients)。

### Claude Code 安装

**方式一：npx skills CLI（推荐）**

```bash
npx skills add full-aigc-skills/processon-skills
```

**方式二：手动安装**

```bash
git clone https://github.com/full-aigc-skills/processon-skills.git
cp -r processon-skills/skills/* .claude/skills/
```

## 🔌 宿主集成

技能本体与宿主无关。已知消费方：

- [codex-processon-plugin](https://github.com/partme-ai/codex-processon-plugin)（Codex 插件，经 `skills.lock.json` vendor 本包）
- WorkBuddy ProcessOn 团队（[workbuddy-agent-experts](https://github.com/partme-ai/workbuddy-agent-experts)，构建期 vendor）

## 📄 License

Apache 2.0
