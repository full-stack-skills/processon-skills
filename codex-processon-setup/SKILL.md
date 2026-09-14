---
name: codex-processon-setup
description: 配置或轮换 Codex ProcessOn 插件的本地 Token。首次使用、缺少凭证、凭证失效，或用户询问 ProcessOn Token 设置时使用；不用于创建 Token、管理账号或处理他人凭证。
---

# ProcessOn 本地凭证设置

让用户在本机三步页面完成一次设置，随后由插件自动连接 ProcessOn。整个流程不得在对话、命令参数或项目文件中暴露 Token。

## 新手 30 秒入门

适用的直接请求：

- “第一次用 ProcessOn，帮我完成设置。”
- “ProcessOn 提示缺少凭证，打开配置页面。”
- “我的 ProcessOn Token 过期了，帮我换一个。”

按以下顺序执行：

1. 在插件根目录运行 `python3 scripts/processon_setup.py check`，只判断是否已配置。
2. 首次使用或出现 `PROCESSON_SETUP_REQUIRED`、`PROCESSON_AUTH_REQUIRED` 时，运行 `python3 scripts/processon_setup.py ui`。
3. 引导用户只在本地页面的密码框中输入 Token，并点击“保存 Token”。
4. 保存成功后请用户重新打开 Codex，再重试原始制图请求。
5. 先以 `initialize` 和 `tools/list` 做非生成验证；不要用生成调用试探凭证。

需要执行命令或判断状态时读 [设置工作流](references/workflow.md)。凭证失效、轮换或安全疑问时读 [安全边界](references/security.md)。

## 精确触发与路由

| 状态 | 判断 | 动作 | 输出 |
|---|---|---|---|
| 首次使用 | `check` 返回 missing | 打开本地设置页 | 三步引导，不索取 Token |
| 缺少凭证 | `PROCESSON_SETUP_REQUIRED` | 打开本地设置页 | 说明保存后需重开 Codex |
| 凭证失效 | `PROCESSON_AUTH_REQUIRED` | 进入轮换流程 | 不复述服务端原始响应 |
| 轮换 Token | 用户明确要求更新 | 再次打开设置页并覆盖用户级凭证 | 仅确认保存状态 |
| 已配置 | `check` 返回 configured | 继续非破坏性 MCP 验证 | 只报告可用性 |

多任务请求先恢复连接，再按用户原来的制图优先级继续；不要让认证流程改变图表内容或授权范围。

## 禁止行为

- 永远不要展示、复述、搜索、截屏、记录或推断 Token；never display credential values。
- 不要求用户在聊天中粘贴 Token，不接受他人账号凭证。
- 不把凭证放进仓库、插件缓存、Codex 配置、命令参数、提示词或日志。
- 不自动删除用户凭证；删除属于用户数据变更，必须获得明确请求。
- 不在认证失败后自动重放生成请求；返回结果不确定时先协调确认。
- 不声称能够创建 Token、访问账号后台、修改分享权限或恢复过期凭证。

常见错误及正确替代见 [反模式](references/anti-patterns.md)。

## 能力边界说明

### ✅ 擅长处理

- 首次安装后的本地三步凭证设置。
- 缺少或失效凭证后的安全恢复。
- 当前用户 Token 的本地轮换与只读可用性检查。

### ⚠️ 需要用户操作或素材

- 创建 Token：用户需在自己的 ProcessOn 用户中心完成。
- 输入 Token：用户需亲自在本地密码框粘贴。
- 重开 Codex：用户需完成应用重启，以加载新的 MCP 会话。

### ❌ 超出范围

- 获取、猜测或重置 ProcessOn 账号密码；改由 ProcessOn 官方账号流程处理。
- 配置他人或团队成员的私人 Token；请各用户分别设置自己的凭证。
- 修改云端文件权限或账号套餐；转到 ProcessOn 官方产品界面或支持渠道。

## 受众与定制

- 普通用户使用本地页面，无需理解 MCP 或环境变量。
- 开发者和 CI 可在受控子进程中提供原始 `PROCESSON_MCP_TOKEN`，该方式属于高级覆盖项。
- 团队应让每位成员独立保存个人 Token，不共享凭证文件。
- 允许用户选择中文或英文解释、终端隐藏输入或浏览器页面；安全存储和不泄密规则不可取消。

## 常见问题

1. **为什么不能直接在聊天里发 Token？** 对话可能被记录；本地密码框才是指定输入面。
2. **保存在哪里？** 保存在当前用户配置目录，不在插件安装目录；具体路径见安全参考。
3. **插件升级后还在吗？** 在。凭证与版本化插件缓存分离。
4. **可以粘贴带 `Bearer` 的值吗？** 可以，设置程序会规范化后只保存原始 Token。
5. **为什么保存后要重开 Codex？** 新任务需要重新启动 stdio MCP 会话并读取凭证。
6. **认证失败会自动重复生成吗？** 不会。只允许一次认证刷新，生成结果不确定时不重放。

边缘场景、兼容性、商用与合规问题见 [深度 FAQ](references/faq-deep.md)。完整交互样例见 [使用示例](references/examples.md)。

## 输出准确性

只报告 `configured`、`missing`、需要重新设置或非破坏性验证结果。无法确认的运行状态必须明确标为未验证，禁止编造凭证路径、Token 状态、工具清单或 ProcessOn 账号能力。
