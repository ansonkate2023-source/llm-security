# AI Security 總覽

## 每日報告索引

| 日期 | 報告 | 重點 |
|------|------|------|
| 2026-04-06 | [daily-report.md](2026-04-06/daily-report.md) | Prompt injection 激增 340%、MCP 30+ CVE、LRM 自主 jailbreak、AI Agent 安全危機 |

## 知識庫

### 攻擊手法 (`/knowledge/attacks/`)
- [Prompt Injection](../knowledge/attacks/prompt-injection.md) — LLM 最高風險漏洞
- [Jailbreak](../knowledge/attacks/jailbreak.md) — LLM 護欄繞過技術
- [MCP 漏洞](../knowledge/attacks/mcp-vulnerabilities.md) — Model Context Protocol 安全危機
- [AI Agent 攻擊](../knowledge/attacks/ai-agent-attacks.md) — Agent 系統安全威脅
- [資料外洩](../knowledge/attacks/data-exfiltration.md) — LLM/RAG 資料外洩攻擊
- [模型投毒](../knowledge/attacks/model-poisoning.md) — 訓練資料投毒與後門攻擊
- [幻覺利用](../knowledge/attacks/hallucination-exploitation.md) — AI 幻覺的安全利用（Slopsquatting）
- [供應鏈攻擊](../knowledge/attacks/supply-chain-attacks.md) — AI 框架與套件供應鏈入侵
- [RAG 投毒](../knowledge/attacks/rag-poisoning.md) — RAG 管道知識庫投毒攻擊與防禦
- [真實事件](../knowledge/attacks/real-world-incidents.md) — 2026 年真實世界 AI 安全事件彙整
- [Shadow AI](../knowledge/attacks/shadow-ai.md) — 企業未授權 AI 使用風險
- [模型竊取](../knowledge/attacks/model-theft.md) — API 萃取、硬體攻擊、模型指紋防禦
- [AI 驅動攻擊](../knowledge/attacks/offensive-ai.md) — AI 武器化、深偽、自主網路攻擊
- [不安全輸出處理](../knowledge/attacks/insecure-output-handling.md) — LLM 輸出導致 XSS/SSRF/RCE

### 防禦策略 (`/knowledge/defenses/`)
- [Prompt Injection 防禦](../knowledge/defenses/prompt-injection-defense.md) — 多層防禦策略
- [沙箱與隔離](../knowledge/defenses/sandbox-isolation.md) — AI Agent 沙箱化技術與 Zero Trust
- [權限控制與審計](../knowledge/defenses/permission-audit.md) — RBAC、審計日誌、OWASP 權限風險
- [自動化決策治理](../knowledge/defenses/autonomous-decision-governance.md) — Agent 自主決策風險與治理框架

### 工具與框架 (`/knowledge/tools/`)
- [Red Teaming 工具](../knowledge/tools/red-teaming-tools.md) — 紅隊測試工具與安全框架
- [防禦工具](../knowledge/tools/defense-tools.md) — Agent 治理、沙箱平台、安全掃描
