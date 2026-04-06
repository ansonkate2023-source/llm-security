# MCP 安全防禦指南

**分類：** defense
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

MCP（Model Context Protocol）在 2026 年成為 AI agent 最主要的攻擊面之一。OWASP GenAI Security Project 於 2026 年 2 月發布「MCP Server 安全開發實務指南」。Dark Reading 指出 MCP 安全「無法靠補丁解決」— 需要架構級防禦。

## OWASP MCP 安全風險

### Tool Poisoning（工具投毒）
- 在工具描述或 metadata 中嵌入惡意指令
- AI 模型被欺騙執行非預期操作（如資料外洩）
- 使用者不會察覺
- **偵測工具：** mcp-scan

### Rug Pull（信任背叛）
- 工具描述或行為在使用者批准後被靜默修改
- 攻擊者先建立信任，再利用隱藏指令操控行為
- 使用者無法感知變更

### Cross-Origin Escalation（跨源提權）
- 跨 MCP server 的權限提升
- 利用不同 server 間的信任關係

### Prompt Injection via External Data
- 透過不受信任的外部內容源注入
- MCP 連接的資料源成為攻擊入口

### Supply Chain Attack
- 惡意 MCP server 偽裝為合法服務
- 在註冊中心發佈惡意套件

## 防禦架構（Defense-First）

### 輸入層
```
使用者請求 → [輸入驗證] → [意圖分類] → MCP Router
```
- 驗證所有使用者輸入
- 分類請求意圖
- 阻擋已知攻擊模式

### 工具層
```
MCP Router → [工具描述驗證] → [能力限制] → Tool Execution
```
- 驗證工具描述完整性（偵測 poisoning）
- 限制工具能力範圍
- 沙箱執行

### 輸出層
```
Tool Response → [輸出過濾] → [資料遮罩] → 使用者
```
- 過濾工具回應中的惡意內容
- 遮罩敏感資料
- 驗證輸出格式

### 監控層
- 持續監控工具描述變更（偵測 rug pull）
- 追蹤異常的工具呼叫模式
- 告警跨源存取嘗試

## 安全工具

### mcp-scan（Invariant Labs）
- **功能：** MCP 標準安全掃描器
- **偵測：** Tool poisoning、rug pull、cross-origin escalation、prompt injection
- **來源：** [Invariant Labs](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks)

### Straiker MCP Security
- **功能：** MCP 安全防護平台
- **來源：** [Straiker](https://www.straiker.ai/solution/mcp-security)

## CyberArk 研究：「到處都是毒」

CyberArk 研究發現 MCP server 的**所有輸出**都可能被投毒 — 不僅是工具描述，還包括回應內容、錯誤訊息等。
- **來源：** [CyberArk](https://www.cyberark.com/resources/threat-research-blog/poison-everywhere-no-output-from-your-mcp-server-is-safe)

## Elastic Security Labs 建議

針對自主 agent 的 MCP 工具攻擊向量與防禦建議：
- **來源：** [Elastic Security Labs](https://www.elastic.co/security-labs/mcp-tools-attack-defense-recommendations)

## 開發者安全清單

- [ ] 使用 mcp-scan 掃描所有 MCP server
- [ ] 驗證工具描述未被篡改
- [ ] 實施工具能力最小化
- [ ] 監控工具描述變更
- [ ] 沙箱執行所有工具
- [ ] 清理所有工具輸出
- [ ] 驗證 MCP server 來源與完整性
- [ ] 實施速率限制
- [ ] 記錄所有工具呼叫以供審計

## 參考

- [OWASP — MCP Server Security Guide](https://mcpplaygroundonline.com/blog/mcp-security-tool-poisoning-owasp-top-10-mcp-scan)
- [Dark Reading — MCP Security Can't Be Patched](https://www.darkreading.com/application-security/mcp-security-patched)
- [Christian Schneider — Securing MCP Defense-First](https://christian-schneider.net/blog/securing-mcp-defense-first-architecture/)
- [CyberArk — Poison Everywhere](https://www.cyberark.com/resources/threat-research-blog/poison-everywhere-no-output-from-your-mcp-server-is-safe)
- [Elastic — MCP Attack Vectors](https://www.elastic.co/security-labs/mcp-tools-attack-defense-recommendations)
- [FlowHunt — MCP Tool Poisoning and Rug Pulls](https://www.flowhunt.io/blog/mcp-tool-poisoning-rug-pulls-safe-tool-design/)
