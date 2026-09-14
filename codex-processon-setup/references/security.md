# 安全边界

## 存储位置

- macOS/Linux：`$XDG_CONFIG_HOME/processon/credentials.json`，未设置时为 `~/.config/processon/credentials.json`。
- Windows：`%APPDATA%\processon\credentials.json`。
- Unix 目录权限为 `0700`，文件权限为 `0600`。
- `PROCESSON_CONFIG_PATH` 仅用于隔离测试或受控高级部署。

## 数据流

本地页面把用户输入提交到同一 loopback 服务。设置程序将原始 Token 原子保存到用户目录。stdio 代理读取 Token，为发往 `https://smart-hd.processon.com/mcp` 的请求添加 `Authorization: Bearer`，不会把 Token 发送给其他来源。

## 轮换与失败

轮换时重新运行 `python3 scripts/processon_setup.py ui`，保存新值并重开 Codex。HTTP 401 只触发一次本地重新读取；第二次失败转为 `PROCESSON_AUTH_REQUIRED`。生成调用遇到连接中断、408 或 5xx 时状态未知，必须停止并协调，不能盲目重放。

## 隐私检查

- 只检查凭证是否存在，不读取或输出其内容。
- 不在截图、剪贴板记录、终端参数、异常堆栈或验收报告中留下 Token。
- 真实验收只记录时间、协议结果、工具名和非敏感产物标识。
- 用户要求删除凭证时，先确认准确用户级路径和可恢复性，再单独执行。
