# Codex Live Token Cost — DeepSeek 增强版

在 [Codex](https://github.com/openai/codex) 输入框上方实时显示 Token 用量、花费以及 **DeepSeek 账户余额**，支持峰谷时段自动双倍计价。

> 基于 [Tianzora/codex-token-cost](https://github.com/Tianzora/codex-token-cost) v0.6.0 修改。

---

## ✨ 功能

- **实时 Token 统计** — 本轮输入/输出、会话总量、缓存命中率
- **DeepSeek 余额查询** — 每 60 秒自动刷新，余额变动带滚动动画
- **峰谷定价** — 北京时间 9:00–12:00 / 14:00–18:00 自动按 2 倍计费
- **本轮花费** — 实时显示当前轮次的 token 费用
- **会话花费** — 累计整个会话的花费
- **可隐藏花费** — 设置面板可分别隐藏「本轮花费」「会话花费」
- **本地统计资料** — 解锁官方个人资料页并替换为本地累计统计

### 支持模型

| 模型 | 输入 (cache miss) | 输入 (cache hit) | 输出 | 计费货币 |
|------|-------------------|-----------------|------|---------|
| `deepseek-v4-flash` | ¥1 / 1M | ¥0.02 / 1M | ¥2 / 1M | ¥ (CNY) |
| `deepseek-v4-pro` | ¥3 / 1M | ¥0.025 / 1M | ¥6 / 1M | ¥ (CNY) |
| `gpt-5.3-codex` | $1.75 / 1M | $0.175 / 1M | $14 / 1M | $ (USD) |
| `gpt-5.4` | $2.50 / 1M | $0.25 / 1M | $15 / 1M | $ (USD) |
| `gpt-5.4-mini` | $0.75 / 1M | $0.075 / 1M | $4.50 / 1M | $ (USD) |
| `gpt-5.5` | $5 / 1M | $0.50 / 1M | $30 / 1M | $ (USD) |
| `gpt-5.5-pro` | $30 / 1M | — | $180 / 1M | $ (USD) |

> DeepSeek 高峰期（北京时间每日 9:00–12:00、14:00–18:00）价格 ×2，适用所有计费项。

---

## 📦 部署

### 方式一：直接复制脚本

1. 下载 `scripts/market-codex-live-token-cost.js`
2. 放入 Codex++ 用户脚本目录：

   ```
   %APPDATA%\Codex++\user_scripts\
   ```

3. 重启 Codex

### 方式二：命令行一键部署

```powershell
Copy-Item .\scripts\market-codex-live-token-cost.js "$env:APPDATA\Codex++\user_scripts\market-codex-live-token-cost.js" -Force
```

---

## ⚙️ 配置

### 设置 DeepSeek API Key

1. 打开 Codex，点击输入框上方的齿轮按钮 ⚙
2. 在「API 密钥」区域输入你的 [DeepSeek API Key](https://platform.deepseek.com/api_keys)
3. 点击「保存」

保存后 HUD 会自动显示「余额 ¥XX.XX」并每 60 秒刷新。

### 获取 DeepSeek API Key

前往 [DeepSeek 开放平台](https://platform.deepseek.com/api_keys) 创建 API Key。

### 隐藏花费显示

在设置面板「显示选项」中勾选「隐藏本轮花费」或「隐藏会话花费」。

### 自定义模型价格

在设置面板「模型价格」区域可自定义任意模型的输入/缓存/输出价格。

---

## 🖥 HUD 布局

```
本轮 输入 1.4M 输出 4.8K | 会话 28M | 缓存 25M(88%) | 本轮花费 ¥0.00 | 会话花费 ¥0.00 | 余额 ¥76.56 | deepseek-v4-flash
```

---

## 🔧 技术说明

- DeepSeek 余额通过 `electronBridge.sendMessageFromView` 代理请求（Codex Electron 的 CSP 策略阻止直接 fetch）
- 余额查询接口：`GET https://api.deepseek.com/user/balance`
- 定价参考：[DeepSeek API 定价文档](https://api-docs.deepseek.com/zh-cn/quick_start/pricing)
- 峰谷时段基于本地系统时间（UTC+8）判断

---

## 📄 License

MIT — 基于 [Tianzora/codex-token-cost](https://github.com/Tianzora/codex-token-cost) 修改。
