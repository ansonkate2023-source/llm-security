# AI 防禦工具與平台

**分類：** tool
**最後更新：** 2026-04-07

## Agent 治理與安全

### Microsoft Agent Governance Toolkit
- **類型：** 開源
- **發布：** 2026-04-02
- **功能：** 涵蓋 OWASP Agentic AI Top 10 所有風險的運行時安全治理
- **特點：** 無狀態策略引擎（< 0.1ms 延遲）、DID 身份、執行環、斷路器
- **整合：** LangChain、CrewAI、Microsoft Agent Framework
- **語言支援：** Python、TypeScript、Rust、Go、.NET
- **新增整合：** OpenAI Agents SDK、Haystack、LangGraph、PydanticAI（已發布至 PyPI）
- **來源：** [Microsoft Open Source Blog](https://opensource.microsoft.com/blog/2026/04/02/introducing-the-agent-governance-toolkit-open-source-runtime-security-for-ai-agents/) / [Help Net Security](https://www.helpnetsecurity.com/2026/04/03/microsoft-ai-agent-governance-toolkit/)

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

### Sage — AI Agent OS 安全層
- **類型：** 開源
- **功能：** 在 AI agent 與 OS 之間放置安全層
- **來源：** [Help Net Security](https://www.helpnetsecurity.com/2026/03/09/open-source-tool-sage-security-layer-ai-agents/)

### TrinityGuard — 多 Agent 風險分類
- **類型：** 開源
- **功能：** 三層風險分類法，AG2/AutoGen 整合
- **適用：** 多 agent 系統安全治理

### Cisco DefenseClaw
- **類型：** 開源
- **發布：** RSAC 2026
- **安裝：** 約 5 分鐘
- **功能：** 掃描 AI agent 使用的 MCP 工具、plugin、資源的安全漏洞
- **特點：**
  - 追蹤 MCP 資源變更以捕捉新漏洞
  - 2 秒內封鎖 MCP server（無需重啟 agent）
  - 撤銷沙箱權限並隔離檔案
  - 掃描 AI 生成程式碼的惡意碼，結果自動發送至 Splunk
- **Duo IAM 整合：** 註冊 AI agent、限制工具存取、唯讀/修改權限、時間窗口限制
- **來源：** [SiliconANGLE](https://siliconangle.com/2026/03/23/cisco-debuts-new-ai-agent-security-features-open-source-defenseclaw-tool/)

### Allama — AI 安全自動化平台
- **類型：** 開源
- **功能：** AI 安全自動化
- **來源：** [Help Net Security](https://www.helpnetsecurity.com/2026/02/09/allama-open-source-ai-security-automation-platform/)

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

## AI Coding Agent 偵測

### Sysdig Falco Rules for AI Coding Agents
- **類型：** 開源
- **發布：** 2026-04-07
- **功能：** 透過 eBPF/Falco 在 syscall 層級偵測 AI coding agent 運行行為
- **支援：** Claude Code（Bun binary）、Gemini CLI（Node.js）、Codex CLI（Rust binary）
- **偵測：** config 目錄存取（~/.claude/, ~/.gemini/, ~/.codex/）中的 API token 和 session 資料
- **應用：** 開發工作站和 CI/CD 環境的運行時可見性
- **來源：** [Sysdig Blog](https://www.sysdig.com/blog/ai-coding-agents-are-running-on-your-machines-do-you-know-what-theyre-doing)

### STSS（SHA-256 Merkle Tree Skill 驗證）
- **類型：** 開源
- **功能：** Agent skill 靜態分析和行為審計
- **技術：** SHA-256 Merkle tree 密碼學驗證 skill 完整性
- **開發者：** Adversa AI（RSA 2026 最具創新性獎項得主）
- **來源：** [Adversa AI](https://adversa.ai/blog/top-agentic-ai-security-resources-april-2026/)

### Mindgard CART
- **類型：** 商用
- **功能：** 持續自動化紅隊測試（Continuous Automated Red Teaming）
- **評價：** RSA 2026 評選最佳 AI 安全工具
- **來源：** [Mindgard](https://mindgard.ai)

## 安全框架更新（Q2 2026）

### OWASP AI Security Solutions Landscape Q2 2026
- Agentic AI 安全解決方案完整版圖
- 涵蓋所有主要 agentic AI 安全供應商和工具
- 來源：[OWASP](https://genai.owasp.org/resource/ai-security-solutions-landscape-for-agentic-ai-q2-2026/)

### OWASP GenAI Data Security 2026
- GenAI 資料安全風險與緩解指南
- 來源：[OWASP](https://genai.owasp.org/resource/owasp-genai-data-security-risks-mitigations-2026/)

## 參考

- [Microsoft — Agent Governance Toolkit](https://opensource.microsoft.com/blog/2026/04/02/introducing-the-agent-governance-toolkit-open-source-runtime-security-for-ai-agents/)
- [Cloudflare — Dynamic Workers](https://www.infoq.com/news/2026/04/cloudflare-dynamic-workers-beta/)
- [InfoQ — Claude Firefox Vulnerabilities](https://www.infoq.com/news/2026/03/claude-ai-firefox-vulnerability/)
- [Cisco — Agentic Workforce Security](https://newsroom.cisco.com/c/r/newsroom/en/us/a/y2026/m03/cisco-reimagines-security-for-the-agentic-workforce.html)
- [Sysdig — AI Coding Agents Detection](https://www.sysdig.com/blog/ai-coding-agents-are-running-on-your-machines-do-you-know-what-theyre-doing)
- [Adversa AI — Agentic AI Security Resources](https://adversa.ai/blog/top-agentic-ai-security-resources-april-2026/)
- [OWASP — AI Security Solutions Landscape Q2 2026](https://genai.owasp.org/resource/ai-security-solutions-landscape-for-agentic-ai-q2-2026/)
