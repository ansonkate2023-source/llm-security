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

## 參考

- [Microsoft — Agent Governance Toolkit](https://opensource.microsoft.com/blog/2026/04/02/introducing-the-agent-governance-toolkit-open-source-runtime-security-for-ai-agents/)
- [Cloudflare — Dynamic Workers](https://www.infoq.com/news/2026/04/cloudflare-dynamic-workers-beta/)
- [InfoQ — Claude Firefox Vulnerabilities](https://www.infoq.com/news/2026/03/claude-ai-firefox-vulnerability/)
