# MCP（Model Context Protocol）安全漏洞

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

MCP 生態系統在 2026 年 1-2 月期間累積超過 30 個 CVE。82% 的實作存在路徑遍歷漏洞，67% 有程式碼注入風險，38-41% 缺乏認證機制。

## 重要 CVE

| CVE ID | 嚴重性 | 類型 | 說明 |
|--------|--------|------|------|
| CVE-2025-49596 | Critical | RCE | MCP Inspector 工具包含遠端程式碼執行漏洞 |
| CVE-2025-6514 | CVSS 9.6 | Command Injection | mcp-remote 命令注入，影響 437,000+ 下載 |
| CVE-2025-54136 | High | Trust Bypass | Cursor IDE 信任機制缺陷，批准後不再重新驗證 |

## 攻擊模式分佈

1. **Exec/Shell Injection**（43%）— 未清理使用者輸入直接傳遞至 shell 命令
2. **工具基礎設施缺陷**（20%）
3. **認證繞過**（13%）
4. **路徑遍歷**（10%）
5. **其他**（14%）— SSRF、跨租戶暴露、供應鏈攻擊

## 五大核心攻擊模式

### Tool Poisoning
在 MCP 工具描述中注入惡意指令。

### Prompt Injection via External Data
利用不受信任的外部內容源進行注入。

### Trust Bypass
在使用者批准後靜默修改 MCP server 設定。

### Supply Chain Attack
在套件註冊中心發佈冒充合法服務的惡意套件。

### Cross-Tenant Exposure
在共享基礎設施中突破隔離邊界。

## 防禦策略

1. 輸入清理 — 所有使用者輸入在傳遞至 shell 前必須清理
2. 認證強化 — 所有 API endpoint 必須要求認證
3. 持續信任驗證 — 每次使用時重新驗證 server 設定
4. 供應鏈審計 — 驗證套件來源與完整性
5. 租戶隔離 — 嚴格的沙箱與隔離機制

## 參考

- [MCP Security 2026: 30 CVEs in 60 Days](https://www.heyuan110.com/posts/ai/2026-03-10-mcp-security-2026/)
