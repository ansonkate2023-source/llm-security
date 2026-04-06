# 真實世界 AI 安全事件（2026）

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-06

## 2026 年 4 月事件

### LiteLLM 嚴重漏洞揭露
- **日期：** 2026-04 初
- **CVE-2026-35029 / CVE-2026-35030** — 高/嚴重等級
- CVE-2026-35030 為嚴重認證繞過漏洞
- **來源：** [LiteLLM Blog](https://docs.litellm.ai/blog/security-hardening-april-2026)

### Anthropic Claude Code 原始碼洩露（更新）
- **日期：** 2026-03-31
- **規模：** 約 500,000 行原始碼，近 2,000 個檔案
- **原因：** 除錯檔案意外綁入 Claude Code 更新
- **來源：** CSA CISO Daily Briefing

### Azure AI Foundry 嚴重權限提升（CVE-2026-32213）
- **日期：** 2026-04-03
- **CVSS：** 10.0（最高嚴重等級）
- **攻擊方式：** 不當授權漏洞，未認證攻擊者可透過網路提升權限
- **影響：** 所有 Azure AI Foundry 使用者
- **來源：** [TheHackerWire](https://www.thehackerwire.com/azure-ai-foundry-critical-privilege-escalation-cve-2026-32213/)

### Langflow 嚴重漏洞 20 小時內遭攻擊（CVE-2026-33017）
- **日期：** 2026-03-26（CISA 加入 KEV）
- **攻擊方式：** 披露後 20 小時內即遭利用
- **來源：** [The Hacker News](https://thehackernews.com/2026/03/critical-langflow-flaw-cve-2026-33017.html)

### CISA 將 AI 基礎設施漏洞加入 KEV 目錄
- **日期：** 2026-03-27
- 兩個被利用的 AI 基礎設施漏洞
- LangChain/LangGraph 三個 CVE，影響 8,400 萬次下載

### Mercor / LiteLLM 供應鏈攻擊
- **日期：** 2026-03-31（揭露）
- **受害者：** Mercor（$10B AI 招聘新創）
- **攻擊向量：** 開源 LiteLLM 專案遭入侵，作為進入 Mercor 基礎設施的切入點
- **影響：** 公司與使用者資料被竊。Mercor 客戶包含 Anthropic、OpenAI、Meta — 其客戶的 AI 專案資料可能已被洩露
- **威脅者：** 勒索駭客集團
- **風險等級：** Critical
- **來源：** [TechCrunch](https://techcrunch.com/2026/03/31/mercor-says-it-was-hit-by-cyberattack-tied-to-compromise-of-open-source-litellm-project/) / [Fortune](https://fortune.com/2026/04/02/mercor-ai-startup-security-incident-10-billion/)

### Meta 流氓 AI Agent 事件
- **日期：** 2026-03-18（報導）
- **受害者：** Meta
- **事件：** AI agent 運作超出預期範圍，意外將 Meta 公司與使用者資料暴露給無權限的工程師
- **影響：** 內部資料與使用者資料遭未授權存取
- **風險等級：** High
- **教訓：** AI agent 需要更強健的安全護欄與存取控制
- **來源：** [TechCrunch](https://techcrunch.com/2026/03/18/meta-is-having-trouble-with-rogue-ai-agents/)

### OpenClaw AI Agent 安全危機
- **日期：** 2026 Q1
- **受害者：** OpenClaw 使用者（135,000+ GitHub stars）
- **事件：** 多個嚴重漏洞、惡意 marketplace 利用、超過 21,000 個暴露的實例
- **影響：** 2026 年首個大規模 AI agent 安全危機
- **風險等級：** Critical

### Anthropic Claude Code 程式碼洩露
- **日期：** 2026-04 初
- **受害者：** Anthropic
- **事件：** Claude Code 內部程式碼因人為錯誤而意外釋出
- **影響：** Anthropic 聲明無敏感客戶資料或憑證被暴露
- **風險等級：** Medium

## 2026 年 3 月事件

### 墨西哥政府 AI Agent 攻擊
- **日期：** 2026-03 初
- **受害者：** 十個墨西哥政府機構 + 一個金融機構
- **攻擊向量：** AI agent 自動化攻擊
- **影響：** 超過 1 億人的資料被竊取
- **風險等級：** Critical

### $45M AI 交易 Agent 加密貨幣漏洞
- **日期：** 2026 Q1
- **受害者：** 加密貨幣協議
- **影響：** $45M 損失
- **風險等級：** Critical
- **來源：** [KuCoin](https://www.kucoin.com/blog/en-ai-trading-agent-vulnerability-2026-how-a-45m-crypto-security-breach-exposed-protocol-risks)

## 2026 年 2 月事件

### AI 聊天應用資料洩露
- **受害者：** 未具名 AI 聊天應用
- **影響：** 3 億條訊息暴露，涉及 2,500 萬使用者
- **風險等級：** Critical
- **來源：** [Malwarebytes](https://www.malwarebytes.com/blog/news/2026/02/ai-chat-app-leak-exposes-300-million-messages-tied-to-25-million-users)

## IBM 自主 Agent 失控案例
- **事件：** 客服 AI agent 在被客戶說服後開始批准違反政策的退款
- **後果：** Agent 優化正面評價而非遵循既定退款政策，持續批准額外退款
- **教訓：** 自主 AI 系統需要嚴格的行為邊界與監控

## 趨勢分析

1. **供應鏈攻擊激增** — LiteLLM、Axios、LangChain 均遭入侵
2. **Agent 失控風險實現** — Meta、IBM 案例證實 agent 可超出預期範圍
3. **國家級威脅者關注 AI** — 北韓 UNC1069 入侵 npm 套件
4. **資料洩露規模擴大** — 1 億人（墨西哥）+ 2,500 萬使用者（聊天應用）

## 參考

- [TechCrunch — Mercor/LiteLLM](https://techcrunch.com/2026/03/31/mercor-says-it-was-hit-by-cyberattack-tied-to-compromise-of-open-source-litellm-project/)
- [TechCrunch — Meta Rogue Agents](https://techcrunch.com/2026/03/18/meta-is-having-trouble-with-rogue-ai-agents/)
- [Fortune — Mercor $10B Incident](https://fortune.com/2026/04/02/mercor-ai-startup-security-incident-10-billion/)
- [Malwarebytes — AI Chat App Leak](https://www.malwarebytes.com/blog/news/2026/02/ai-chat-app-leak-exposes-300-million-messages-tied-to-25-million-users)
