<div align="center">

# processon-skills

**ProcessOn AIGC 技能 — 流程图、泳道图、UML、架构图、ER 图、思维导图、结构化信息图、生成提示词与审阅契约**

[![GitHub](https://img.shields.io/badge/github-full--stack--skills%2Fprocesson--skills-green.svg)](https://github.com/full-stack-skills/processon-skills)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](LICENSE)
[![Agent Skills](https://img.shields.io/badge/Agent%20Skills-兼容-purple.svg)](https://agentskills.io)

[English](./README.md) | 简体中文

</div>

---

## 📖 简介

**processon-skills** 是一组 AI 编码智能体技能，属于 [Full Stack Skills](https://github.com/full-stack-skills) 生态。包含 **7 个技能**，覆盖"分类 → 建模 → 提示词 → 生成 → 审阅 → 交付"的完整 ProcessOn 制图工作流，经官方 ProcessOn MCP 产出**可编辑**的图形结果。

## 📦 安装

```bash
npx skills add full-stack-skills/processon-skills
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
npx skills add full-stack-skills/processon-skills
```

**方式二：手动安装**

```bash
git clone https://github.com/full-stack-skills/processon-skills.git
cp -r processon-skills/skills/* .claude/skills/
```

## 🔌 宿主集成

技能本体与宿主无关。已知消费方：

- [codex-processon-plugin](https://github.com/partme-ai/codex-processon-plugin)（Codex 插件，经 `skills.lock.json` vendor 本包）
- WorkBuddy ProcessOn 团队（[workbuddy-agent-experts](https://github.com/partme-ai/workbuddy-agent-experts)，构建期 vendor）

<!-- FULL_STACK_DOC_START -->
## 项目定位与边界

`processon-skills` 是包含 **7 个可独立安装 Agent Skill** 的源代码仓库，当前清单版本为 `1.0.1`。本仓负责技能的触发说明、工作流、references、examples 与质量门禁；宿主插件的 Hook、MCP、凭据注入和运行时脚本不属于本仓职责。

| 已确认事实 | 值 | 证据 |
|---|---|---|
| 安装包 | `full-stack-skills/processon-skills` | `.claude-plugin/plugin.json`、仓库远端 |
| 可安装技能 | 7 | `skills/*/SKILL.md` |
| 当前版本 | `1.0.1` | `.claude-plugin/plugin.json` |
| 规格事实源 | OpenSpec | `openspec/config.yaml` |
| 许可证 | Apache-2.0 | `LICENSE` |

### 不负责

- 不替代消费插件中的可执行 Harness、MCP 服务、Hook 或供应商客户端；
- 不把 `SKILL.md` 被复制到目录视为宿主已经发现、触发或成功执行；
- 不自动授权网络调用、付费生成、文件覆盖、上传或发布；
- 不允许消费插件直接修改受 `skills.lock.json` 管理的副本。

## 一眼看懂

```text
用户任务
  │
  ▼
name / description 发现技能
  │
  ▼
读取完整 SKILL.md ──► 按需加载 references / examples / scripts
  │
  ▼
执行领域工作流 ──► 收集验证证据 ──► PASS / FAIL / UNVERIFIED
```

## 已验证的安装与发现

```bash
npx skills add full-stack-skills/processon-skills
npx skills add full-stack-skills/processon-skills --skill processon-diagram
npx skills list --json
```

固定发布版本时使用 GitHub Release/tag，不要把移动的 `main` 当成不可变版本。安装完成后应核对技能数量、名称、资源文件和目标 Agent 列表；Codex、ZCode、Kimi 的真实插件加载仍需分别验证。

## 包结构与加载规则

```text
processon-skills/
├── .claude-plugin/plugin.json   # 包名、版本与技能清单
├── skills/<name>/SKILL.md       # 触发条件与主工作流
├── skills/<name>/references/    # 按任务加载的领域知识
├── skills/<name>/examples/      # 请求、验收与恢复示例
├── scripts/                     # 仓库级生成和质量门禁（若存在）
├── openspec/                    # 规格与归档变更
└── LICENSE
```

跨技能协作必须使用技能名和安装命令，不得依赖 `../sibling-skill/` 相对链接，因为用户可能只安装一个技能。

## 质量、发布与安全

```bash
python3 scripts/lint_skills.py
```

发布前还必须检查 frontmatter、相对链接、资源完整性、TRACE 阈值、版本清单以及干净环境安装。正式 tag 不得移动；内容变化应发布新版本，并让消费插件通过 tag、peeled SHA 和摘要更新锁文件。

安全边界：不得提交真实密钥、账号、本机绝对路径或私有仓库地址；脚本应默认最小权限，付费、上传、删除和覆盖动作必须保留显式授权门。

## 故障排查

| 现象 | 检查 | 处理 |
|---|---|---|
| 安装后未发现技能 | frontmatter、Agent 发现目录、是否需要刷新 | 用 `skills list --json` 核对实际发现结果 |
| 只安装单个技能后引用缺失 | 是否存在跨技能相对路径 | 把必需资源移入当前技能，或按名称安装依赖技能 |
| 插件完整性检查失败 | tag、peeled SHA、摘要和本地技能清单 | 在源技能仓发布新版本，再由同步 PR 更新插件 |
| 工具或凭据缺失 | `compatibility`、运行时前置条件 | 报告 `UNVERIFIED`，不要猜测成功 |
| 自动化第二次运行仍产生差异 | 生成器非幂等或清单漂移 | 阻止发布并修复生成/排序规则 |
<!-- FULL_STACK_DOC_END -->

## 📄 License

Apache 2.0
