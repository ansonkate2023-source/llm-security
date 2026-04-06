# AI Security Daily Report — 2026-04-06

## 1. 今日 AI Security 重點摘要

- Prompt injection 攻擊在 2026 年激增 340%，OWASP 將其列為 LLM 最高嚴重等級漏洞
- MCP（Model Context Protocol）在 60 天內累積 30+ CVE，82% 實作存在路徑遍歷漏洞
- 大型推理模型（LRM）可自主對其他 LLM 執行 jailbreak，成功率達 97.14%
- 97% 企業預期一年內將遭遇重大 AI Agent 安全事件，但僅 6% 安全預算投入此領域
- AI 生成程式碼一週內揭露 35 個 CVE，87% AI PR 被標記安全問題
- LangChain/LangGraph 揭露多個嚴重 CVE（CVSS 最高 9.3），影響數百萬 LLM 應用
- Axios npm 套件遭北韓 UNC1069 入侵，影響數億 JavaScript 專案
- Microsoft 發布 Agent Governance Toolkit 開源工具，涵蓋 OWASP Agentic AI Top 10
- EchoLeak 零點擊攻擊：僅發送電子郵件即可讓 Microsoft 365 Copilot 自主外洩企業資料
- Slopsquatting 新型供應鏈攻擊：利用 AI 幻覺的套件名稱植入後門
- 僅 250 個惡意文件即可在任何規模 LLM 中建立後門（Anthropic 研究）

---

## 2. 高風險項目（必讀）

### CVE-2026-0628 — Chrome Gemini 劫持（Critical）
- **類型：** attack
- **攻擊方式：** Unit 42 發現 Chrome Gemini Live 面板的高嚴重性漏洞，惡意擴充套件可劫持特權 AI 助理並存取攝影機與麥克風
- **影響範圍：** 所有使用 Chrome Gemini 的使用者
- **可利用性：** 高 — 已在野外被利用
- **關鍵字：** Chrome, Gemini, browser extension, privilege escalation

### CVE-2026-5320 — Vanna-AI 認證缺失（High）
- **類型：** attack
- **攻擊方式：** vanna-ai vanna 2.0.2 及以下版本的 Chat API Endpoint 缺乏認證機制，可遠端利用
- **影響範圍：** 使用 Vanna-AI 的開發者與企業
- **可利用性：** 高 — 可遠端觸發
- **關鍵字：** Vanna-AI, missing authentication, API

### MCP 生態系統安全危機（Critical）
- **類型：** attack
- **攻擊方式：** 30+ CVE 在 60 天內被揭露。主要攻擊模式：Exec/Shell Injection（43%）、工具基礎設施缺陷（20%）、認證繞過（13%）、路徑遍歷（10%）
- **影響範圍：** 所有使用 MCP 的 AI 系統與開發者
- **可利用性：** 極高 — 67% 實作存在程式碼注入風險，38-41% 缺乏認證機制
- **關鍵字：** MCP, tool poisoning, prompt injection, supply chain

### Agent Commander 攻擊（Critical）
- **類型：** attack / research
- **攻擊方式：** 透過 prompt injection 將 AI coding agent 轉換為持久性 C2（Command & Control）平台，使自主 agent 成為遠端控制的惡意程式投遞系統
- **影響範圍：** 所有 AI coding agent 使用者
- **可利用性：** 高 — 已有概念驗證
- **關鍵字：** AI agent, C2, prompt injection, persistent backdoor

---

## 3. 新型攻擊手法（Trending）

### 大型推理模型自主 Jailbreak
- **來源：** [Nature Communications](https://www.nature.com/articles/s41467-026-69010-1)
- **摘要：** LRM 可自主產生說服性多輪對話來 jailbreak 其他 LLM，使非專家也能輕易執行攻擊。整體成功率 97.14%
- **風險等級：** Critical
- **涉及系統：** LLM

### JBFuzz — 基於 Fuzzing 的 Jailbreak 框架
- **摘要：** 透過種子收集、變異引擎、目標互動、評估迴圈與回饋整合，對 GPT-4o、Gemini 2.0、DeepSeek-V3 達到約 99% 攻擊成功率
- **風險等級：** Critical
- **涉及系統：** LLM

### 多模態圖像注入攻擊（Image-Based Prompt Injection）
- **來源：** [CSA Labs](https://labs.cloudsecurityalliance.org/research/csa-research-note-image-prompt-injection-multimodal-llm-2026/)
- **摘要：** 在圖像中嵌入視覺化的對抗性指令來劫持多模態 LLM，利用模態間的互動漏洞
- **風險等級：** High
- **涉及系統：** 多模態 LLM / VLM

### UltraBreak — 跨模型通用對抗攻擊
- **來源：** [arXiv](https://arxiv.org/abs/2602.01025)
- **摘要：** 透過視覺層級正則化與語義引導文字監督發現通用對抗模式，可跨模型與攻擊目標遷移
- **風險等級：** High
- **涉及系統：** VLM

### 墨西哥政府 AI Agent 攻擊事件
- **摘要：** 2026 年 3 月，攻擊者使用 AI agent 入侵十個墨西哥政府機構與一個金融機構，竊取超過 1 億人的資料
- **風險等級：** Critical
- **涉及系統：** AI Agent

---

## 4. 防禦策略更新

### OWASP Agentic AI Top 10
- OWASP 發布 agentic AI 風險排名，Microsoft 已在 Copilot Studio 中實作對應防禦措施
- 來源：[Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/2026/03/30/addressing-the-owasp-top-10-risks-in-agentic-ai-with-microsoft-copilot-studio/)

### MCP 安全五大核心防禦
基於 MCP 生態系統的大規模漏洞揭露，建議的防禦策略：
1. **輸入清理（Input Sanitization）** — 針對 43% 的 Shell Injection 攻擊
2. **認證強化** — 38-41% 實作缺乏認證
3. **信任驗證機制** — 防止 Trust Bypass 攻擊
4. **供應鏈審計** — 驗證套件來源與完整性
5. **租戶隔離** — 防止跨租戶資料暴露

### RLM-JB — 新型 Jailbreak 偵測方法
- **來源：** [Silverfort](https://www.silverfort.com/blog/rlm-jb-a-new-approach-to-ai-jailbreak-detection/)
- 針對 LLM jailbreak 的新偵測框架

### EU AI Act 合規期限
- 完整合規要求將於 **2026 年 8 月** 生效，企業需提前準備

---

## 5. 工具與資源推薦

### Red Teaming 框架
| 工具 | 類型 | 說明 |
|------|------|------|
| [PyRIT](https://github.com/Azure/PyRIT) | 開源 | Microsoft 開發，Python AI 風險識別工具 |
| [Garak](https://github.com/NVIDIA/garak) | 開源 | NVIDIA 開發，LLM 漏洞掃描工具 |
| [DeepTeam](https://github.com/confident-ai/deepteam) | 開源 | LLM 紅隊滲透測試框架 |
| Mindgard | 商用 | 2026 年最佳 AI 紅隊軟體，專注生產環境風險 |
| Microsoft AI Red Teaming Agent | 商用 | Azure AI Foundry 整合，生成式 AI 安全測試 |

### 防禦框架
| 框架 | 說明 |
|------|------|
| NIST AI RMF | AI 風險管理框架 |
| MITRE ATLAS | 16 戰術 + 84 技術的 AI 安全分類學 |
| OWASP LLM Top 10 | LLM 安全風險排名 |
| OWASP Agentic AI Top 10 | Agentic AI 風險排名 |

---

## 來源

- [Sombra Inc — LLM Security Risks 2026](https://sombrainc.com/blog/llm-security-risks-2026)
- [OWASP — Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- [CSA Labs — Image Prompt Injection](https://labs.cloudsecurityalliance.org/research/csa-research-note-image-prompt-injection-multimodal-llm-2026/)
- [Nature Communications — LRM Jailbreak](https://www.nature.com/articles/s41467-026-69010-1)
- [MCP Security 2026: 30 CVEs in 60 Days](https://www.heyuan110.com/posts/ai/2026-03-10-mcp-security-2026/)
- [Zenity — AI Agent Threat Landscape 2026](https://zenity.io/resources/white-papers/2026-threat-landscape-report)
- [HBR — AI Agents Act Like Malware](https://hbr.org/2026/03/ai-agents-act-a-lot-like-malware-heres-how-to-contain-the-risks)
- [Security Boulevard — 97% Enterprises Expect AI Agent Incident](https://securityboulevard.com/2026/04/97-of-enterprises-expect-a-major-ai-agent-security-incident-within-the-year/)
- [Microsoft Security Blog — OWASP Agentic AI](https://www.microsoft.com/en-us/security/blog/2026/03/30/addressing-the-owasp-top-10-risks-in-agentic-ai-with-microsoft-copilot-studio/)
- [CyberArk — Jailbreaking Every LLM](https://www.cyberark.com/resources/threat-research-blog/jailbreaking-every-llm-with-one-simple-click)
- [KuCoin — AI Trading Agent $45M Breach](https://www.kucoin.com/blog/en-ai-trading-agent-vulnerability-2026-how-a-45m-crypto-security-breach-exposed-protocol-risks)
