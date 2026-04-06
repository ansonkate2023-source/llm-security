# AI 防禦工具與平台

**分類：** tool
**最後更新：** 2026-04-06

## Agent 治理與安全

### Microsoft Agent Governance Toolkit
- **類型：** 開源
- **發布：** 2026-04-02
- **功能：** 涵蓋 OWASP Agentic AI Top 10 所有風險的運行時安全治理
- **特點：** 無狀態策略引擎（< 0.1ms 延遲）、DID 身份、執行環、斷路器
- **整合：** LangChain、CrewAI、Microsoft Agent Framework
- **來源：** [Microsoft Open Source Blog](https://opensource.microsoft.com/blog/2026/04/02/introducing-the-agent-governance-toolkit-open-source-runtime-security-for-ai-agents/)

## 沙箱與隔離

### E2B
- **類型：** 商用/開源
- **功能：** 專為 AI agent 設計的 MicroVM 沙箱

### Cloudflare Dynamic Workers
- **類型：** 商用（開放測試中）
- **功能：** V8 Isolate 沙箱，AI 生成程式碼安全執行
- **特點：** 毫秒啟動，比容器高 100 倍記憶體效率

### Docker Sandboxes
- **類型：** 實驗性
- **功能：** Docker 官方 AI agent 沙箱方案

## LLM 安全掃描

### BackdoorLLM
- **類型：** 開源
- **功能：** LLM 後門攻擊與防禦基準測試
- **GitHub：** https://github.com/bboylyg/BackdoorLLM

## AI 安全發現

### Claude Opus 4.6（安全研究）
- 在兩週內發現 Firefox 22 個安全漏洞
- 其中 14 個為高嚴重性分類
- 展示 AI 在防禦端的強大能力
- 來源：[InfoQ](https://www.infoq.com/news/2026/03/claude-ai-firefox-vulnerability/)

## Agent 安全框架（新增 2026-04）

### Microsoft Agent Governance Toolkit（更新）
- **語言支援：** Python、TypeScript、Rust、Go、.NET
- **新增整合：** OpenAI Agents SDK、Haystack、LangGraph、PydanticAI（已發布至 PyPI）
- **來源：** [Help Net Security](https://www.helpnetsecurity.com/2026/04/03/microsoft-ai-agent-governance-toolkit/)

### Sage — AI Agent OS 安全層
- **類型：** 開源
- **功能：** 在 AI agent 與 OS 之間放置安全層
- **來源：** [Help Net Security](https://www.helpnetsecurity.com/2026/03/09/open-source-tool-sage-security-layer-ai-agents/)

### TrinityGuard — 多 Agent 風險分類
- **類型：** 開源
- **功能：** 三層風險分類法，AG2/AutoGen 整合
- **適用：** 多 agent 系統安全治理

### Cisco Agentic Workforce Security
- **類型：** 商用
- **功能：** 重新構想 agentic 工作力的安全
- **來源：** [Cisco Newsroom](https://newsroom.cisco.com/c/r/newsroom/en/us/a/y2026/m03/cisco-reimagines-security-for-the-agentic-workforce.html)

## LLM 後門偵測

### Microsoft LLM Backdoor Scanner
- **類型：** 商用/研究
- **功能：** 偵測開源 AI 模型中的後門
- **目標：** 解決依賴第三方 LLM 的企業的關鍵盲點
- **來源：** [The Hacker News](https://thehackernews.com/search/label/LLM%20Security)

## 安全基準測試工具

### MCP-SafetyBench
- **功能：** 基於真實 MCP server 的 LLM 安全評估基準
- 涵蓋五個領域：瀏覽器自動化、金融分析、位置導航、程式碼管理、網路搜尋
- **來源：** [OpenReview](https://openreview.net/forum?id=7XYjeL46co)

### JBDistill — 可更新安全基準
- **功能：** 簡化不同攻擊為可更新的安全測試
- 基準達 81.8% 有效性，可泛化至 13 個評估模型
- **來源：** [JHU / TechXplore](https://techxplore.com/news/2026-03-renewable-benchmark-llm-jailbreak-safety.html)

### mcp-scan（Invariant Labs）
- **功能：** MCP 安全掃描標準工具
- **偵測：** Tool poisoning、rug pull、cross-origin escalation
- **來源：** [Invariant Labs](https://invariantlabs.ai/blog/mcp-security-notification-tool-poisoning-attacks)

## 參考

- [Microsoft — Agent Governance Toolkit](https://opensource.microsoft.com/blog/2026/04/02/introducing-the-agent-governance-toolkit-open-source-runtime-security-for-ai-agents/)
- [Cloudflare — Dynamic Workers](https://www.infoq.com/news/2026/04/cloudflare-dynamic-workers-beta/)
- [InfoQ — Claude Firefox Vulnerabilities](https://www.infoq.com/news/2026/03/claude-ai-firefox-vulnerability/)
- [Cisco — Agentic Workforce Security](https://newsroom.cisco.com/c/r/newsroom/en/us/a/y2026/m03/cisco-reimagines-security-for-the-agentic-workforce.html)
