---
name: processon-setup
description: Configure or rotate the local ProcessOn Token for a ProcessOn MCP integration. Use for first use, missing credential, invalid credential, or when the user asks about ProcessOn Token setup; do not use for creating a Token, managing an account, or handling another user's credential.
---

# ProcessOn Local Credential Setup

Let the user complete one-time setup on a three-step local page; the integration then connects to ProcessOn automatically. The Token must never appear in chat, command arguments, or project files.

## 30-second quick start

Direct requests that fit:

- "First time using ProcessOn, help me finish setup."
- "ProcessOn says the credential is missing, open the configuration page."
- "My ProcessOn Token expired, help me rotate it."
- “第一次使用 ProcessOn，帮我完成本地设置。”
- “ProcessOn 提示缺少凭据，帮我打开配置页。”
- “我的 ProcessOn Token 已失效，帮我安全更换。”

Execute in this order:

1. From the integration root run `python3 scripts/processon_setup.py check` and decide only by the result.
2. On first use, or whenever `PROCESSON_SETUP_REQUIRED` or `PROCESSON_AUTH_REQUIRED` is returned, wait for the MCP proxy to open the local page automatically. It opens at most once per 10-minute cooldown.
3. Only if the browser does not open, run `python3 scripts/processon_setup.py ui` as the manual fallback.
4. Tell the user to paste the Token only into the local page's password field and click "Save Token".
5. After a successful save, retry the original request; restart the host application only if the current MCP process does not reload the credential.
6. Run `initialize` and `tools/list` for a non-generation validation; do not probe the credential with a generation call.

Read [setup workflow](references/workflow.md) when you need to execute commands or interpret state. Read [security boundary](references/security.md) for credential invalidation, rotation, or safety questions.

## Exact triggers and routing

| State | Detection | Action | Output |
|---|---|---|---|
| First use (首次使用) | `check` returns missing | Proxy auto-opens the local setup page | Three-step guide, do not request the Token |
| Missing credential (缺少凭证) | `PROCESSON_SETUP_REQUIRED` | Use the auto-opened page; manual `ui` only as fallback | Retry after saving |
| Invalid credential (凭证失效) | `PROCESSON_AUTH_REQUIRED` | Proxy auto-opens the same page for rotation | Do not repeat the upstream response |
| Rotate Token (轮换 Token) | User explicitly asks to update | Reopen the setup page and overwrite the user-level credential | Confirm only the save state |
| Already configured | `check` returns configured | Continue with non-destructive MCP validation | Report availability only |

For multi-task requests, restore the connection first and then resume the user's original diagram priority; do not let the authentication flow change diagram content or authorization scope.

## Prohibited behaviors

- Never display, repeat, search, screenshot, log, or infer the Token; never display credential values.
- Do not ask the user to paste the Token in chat, and never accept another person's credential.
- Never place the credential in the repository, plugin cache, host application configuration, command arguments, prompts, or logs.
- Never delete a user credential automatically; deletion is a user-data change and requires an explicit request.
- Never auto-replay a generation request after an authentication failure; when the result is uncertain, coordinate first.
- Never claim the ability to create Tokens, access account admin pages, change sharing permissions, or recover an expired credential.

See [anti-patterns](references/anti-patterns.md) for common mistakes and the correct replacement.

## Capability boundary

### ✅ Handles well

- Local three-step credential setup right after installation.
- Safe recovery after a missing or invalid credential.
- Local rotation and read-only availability check for the current user's Token.

### ⚠️ Requires user action or input

- Creating a Token: the user must do this in their own ProcessOn account center.
- Entering the Token: the user must paste it into the local password field themselves.
- Restarting the host application: the user must restart it so the new MCP session loads the credential.

### ❌ Out of scope

- Retrieving, guessing, or resetting a ProcessOn account password; that goes through ProcessOn's official account flow.
- Configuring another person's or team member's private Token; each user should set their own credential.
- Changing cloud file permissions or account plans; that goes through ProcessOn's official product interface or support.

## Audience and customization

- Normal users use the local page and need no understanding of MCP or environment variables.
- Developers and CI may provide a raw `PROCESSON_MCP_TOKEN` inside a controlled child process; that is an advanced override.
- Teams should let each member save their own Token independently and never share credential files.
- The user may choose Chinese or English explanations, a hidden terminal prompt, or the browser page; safe storage and no-disclosure rules are non-negotiable.

## Frequently asked questions

1. **Why can't I just send the Token in chat?** Conversations can be logged; the local password field is the designated input surface.
2. **Where is it saved?** In the current user's config directory, not the plugin install directory; see the security reference for the exact path.
3. **Will it survive a plugin upgrade?** Yes. The credential is stored separately from the versioned plugin cache.
4. **Can I paste a value that already has `Bearer`?** Yes; the setup normalizes it and stores only the raw Token.
5. **Must I restart the host application after saving?** Retry first: the proxy reloads credentials on authentication failure. Restart it only if the current MCP process remains unavailable.
6. **Will an authentication failure auto-retry generation?** No. Only one authentication refresh is allowed, and uncertain results are not replayed.

See [deep FAQ](references/faq-deep.md) for edge cases, compatibility, commercial, and compliance questions. See [usage examples](references/examples.md) for full interaction samples.

## Output accuracy

Report only `configured`, `missing`, the need to reconfigure, or a non-destructive validation result. Any operational state that cannot be confirmed must be labeled unverified. Never fabricate credential paths, Token status, tool inventories, or ProcessOn account capabilities.

<!-- QUALITY_BASELINE_V1 -->
## When to use（什么时候使用）

当用户需要 **配置或诊断本地认证与运行前置条件** 时加载本技能。先从请求中提取目标、输入、约束、交付格式和验收标准；描述摘要为：Configure or rotate the local ProcessOn Token for a ProcessOn MCP integration. Use for first use, missing credential, invalid credential, or when the user asks about ProcessOn Token setup; do not use for creating a Token, managing an account, or handling another user's credential.。

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

检查本地工具、配置位置、权限和当前认证状态；任一关键条件未知时停止在只读阶段。
### Step 3：形成计划

列出将调用的工具、会改变的对象、成功标准以及失败后的安全退出方式。
### Step 4：执行动作

通过受支持的交互入口完成最小配置，并立即清理敏感输入；每个外部调用均保留可关联的状态或回执。
### Step 5：验证交付

只报告可用性、身份范围和脱敏错误，不输出凭据内容，并把事实、推断和未验证项分开陈述。

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

不回显、记录或提交密钥；不替用户创建账户、购买额度或接受条款。 如果请求需要别的技能，不复制其正文；按技能名称进行交接，并保留当前任务上下文。

## Progressive disclosure

- 需要确定输入/输出、状态和授权点时，读取 `references/workflow-contract.md`。
- 需要交付前自检时，读取 `references/validation-checklist.md`。
- 遇到超时、部分成功或恢复场景时，读取 `references/error-recovery.md`。
- 首次运行、拒绝越权和失败恢复分别参考 `examples/happy-path.md`、`examples/boundary-refusal.md`、`examples/failure-recovery.md`。
