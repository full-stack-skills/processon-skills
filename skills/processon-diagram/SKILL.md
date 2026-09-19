---
name: processon-diagram
description: Model professional ProcessOn flowcharts, swimlanes, UML and sequence diagrams, architecture and ER diagrams, organization and equity charts, timelines, and business-analysis diagrams. Use after the ProcessOn router selects a professional diagram rather than a mind map or infographic.
---

# Professional Diagram Modeling

Turn user facts into a topology that `processon-prompt` can express precisely. Focus on relationships and runtime meaning, not decoration.

## Select the diagram family

| User intent | Family | Required model |
|---|---|---|
| Process, decisions, exceptions | Flowchart | start/end, actions, decisions, labeled outcomes |
| Cross-role process | Swimlane | lanes, owners, handoffs, decisions, exceptions |
| Ordered system interaction | Sequence diagram | participants, messages, returns, alternatives, failures |
| System composition or deployment | Architecture | boundaries, components, dependencies, protocols, data/control flows, trust zones |
| Data model | ER diagram | entities, key fields, PK/FK, cardinality, optionality |
| Software types and behavior | UML class/state/use-case/requirement | standard UML semantics for the requested view |
| Reporting hierarchy | Organization chart | roles, reporting lines, groups, vacant/shared roles |
| Ownership or control | Equity/relationship diagram | subjects, percentages or relation labels, direction |
| Milestones and evolution | Timeline | dates/phases, milestones, outcomes |
| Business analysis | SWOT, PEST, pyramid | named dimensions, concise evidence, priority |

Honor an explicit family unless it cannot represent the requested relationship. Explain any necessary mapping.

## Structure workflow

1. Extract facts without changing meaning.
2. Create a compact list of nodes or participants.
3. Define every meaningful relationship and its direction or label.
4. Separate the primary path from exceptions, optional flows, and annotations.
5. Choose orientation and grouping from the topology.
6. Pass the structure to `processon-prompt`.

## Family-specific rules

- **Flowchart:** use one start and at least one explicit end; decisions are questions with labeled outcomes; do not hide error paths in prose.
- **Swimlane:** each action belongs to exactly one accountable lane; show handoffs at lane boundaries; avoid a lane per individual unless required.
- **Sequence:** time runs top to bottom; distinguish synchronous calls, asynchronous messages, replies, loops, and alternatives.
- **Architecture:** default to an architecture block diagram with large labeled components inside explicit layers or boundaries. Show runtime or deployment boundaries, dependencies, protocols, trust zones, data/control direction, resilience, and observability where relevant. Do not use UML class tables, attribute rows, method compartments, or placeholder field types unless the user explicitly requests a class diagram. Never substitute a directory tree.
- **ER:** include only decision-relevant fields; mark primary and foreign keys; label one-to-one, one-to-many, or many-to-many cardinality and optionality.
- **UML:** choose one view that answers the question; do not mix class, state, use-case, and sequence notation on one canvas.
- **Organization/equity:** separate reporting, ownership, governance, and collaboration relations; label ambiguous edges.
- **Timeline:** use a consistent time scale or explicitly label non-linear phases.
- **SWOT/PEST:** facts stay in the correct dimension and are phrased as concise evidence, not slogans.

## Visual constraints

Use a clear reading direction, restrained palette, consistent shapes for equivalent semantics, adequate contrast, short labels, balanced whitespace, and minimal connector crossings. Use semantic colors sparingly for success, warning, risk, or ownership.

## Accuracy, privacy, and boundaries

- Do not invent components, protocols, owners, cardinalities, dates, percentages, or metrics.
- Ask one question only when a missing answer changes topology; otherwise state a conservative assumption.
- Never include credentials, local paths, private identifiers, or unrelated context in the generation prompt.
- If source code or documents are required, inspect them before modeling; a filename list is not architecture evidence.
- If the current MCP cannot edit an existing file, offer a new diagram based on supplied content and disclose the limitation.

## Chinese starter examples

- “画一个包含登录、风控、支付失败和补偿路径的标准流程图。”
- “把产品、算法、后端、测试、运维的 AI 上线流程画成泳道图。”
- “根据当前源码画运行时架构图，标出协议、信任边界、数据流和故障恢复。”

Return the structure model to the router; do not call ProcessOn directly.

<!-- QUALITY_BASELINE_V1 -->
## When to use（什么时候使用）

当用户需要 **为当前请求选择并执行可验证、可恢复的专业工作流** 时加载本技能。先从请求中提取目标、输入、约束、交付格式和验收标准；描述摘要为：Model professional ProcessOn flowcharts, swimlanes, UML and sequence diagrams, architecture and ER diagrams, organization and equity charts, timelines, and business-analysis diagrams. Use after the ProcessOn router selects a professional diagram rather than a mind map or infographic.。

## Rules

- 先读后写：先确认当前状态与真实能力，再执行会改变外部状态的动作。
- 权限最小化：只使用完成当前步骤所需的文件、工具、账户与网络范围。
- 证据优先：运行结果、资源 ID、版本、哈希或测试输出缺失时，明确标记为 `NOT_VERIFIED`。
- 幂等优先：保留请求标识与阶段状态；结果不明确时先查询，不进行盲目重试。
- 隐私安全：日志、示例、回执和错误信息不得包含 token、cookie、密钥或个人敏感数据。

## Workflow

### Step 1：澄清意图

确认本技能是否匹配目标；若只是相邻需求，交给更精确的技能。
### Step 2：执行预检

确认目标、输入、约束、可用工具、成功标准和失败边界；任一关键条件未知时停止在只读阶段。
### Step 3：形成计划

列出将调用的工具、会改变的对象、成功标准以及失败后的安全退出方式。
### Step 4：执行动作

按最小充分步骤执行，并在关键状态变化处记录证据；每个外部调用均保留可关联的状态或回执。
### Step 5：验证交付

输出结果、验证证据、未完成项、风险和明确的下一步，并把事实、推断和未验证项分开陈述。

## Validation checklist

- [ ] 技能触发条件与用户意图一致，没有把相邻任务误路由到本技能。
- [ ] 输入、目标对象、版本和输出位置均已明确，且没有使用猜测值替代必填值。
- [ ] 所有写入、付费、发布或不可逆动作都在用户授权范围内。
- [ ] 结果已用独立检查验证；仅有“命令成功”或“文件存在”不算完整验收。
- [ ] 输出包含实际证据、失败/跳过项、剩余风险和可执行的下一步。

## Gotchas

1. **把计划当结果**：文档或提示词不等于真实执行；必须标明实际运行层级。
2. **错误重试**：超时或响应丢失可能已经产生远端状态，先查询再决定是否重试。
3. **隐式扩大范围**：批量、全量、发布、覆盖和付费不是普通读写的自然延伸。
4. **版本漂移**：引用外部资源时记录版本、tag 或提交；不要把可变分支当发布证据。
5. **证据过期**：缓存、旧截图和历史测试不能证明当前环境；在交付前刷新关键证据。

## 不适用与边界

不超出用户给定范围；写入、付费、发布和不可逆动作需要明确授权。 如果请求需要别的技能，不复制其正文；按技能名称进行交接，并保留当前任务上下文。

## Progressive disclosure

- 需要确定输入/输出、状态和授权点时，读取 `references/workflow-contract.md`。
- 需要交付前自检时，读取 `references/validation-checklist.md`。
- 遇到超时、部分成功或恢复场景时，读取 `references/error-recovery.md`。
- 首次运行、拒绝越权和失败恢复分别参考 `examples/happy-path.md`、`examples/boundary-refusal.md`、`examples/failure-recovery.md`。
