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
- [Promptware Kill Chain](../knowledge/attacks/promptware-kill-chain.md) — 七階段 AI 攻擊鏈框架
- [攻擊趨勢分析](../knowledge/attacks/attack-trends-analysis.md) — 2026 Q1 攻擊統計與趨勢
- [OpenClaw 安全危機](../knowledge/attacks/openclaw-crisis.md) — 2026 首個大規模 AI agent 安全危機深度分析
- [微調安全攻擊](../knowledge/attacks/fine-tuning-attacks.md) — 10 個樣本 / $0.20 即可移除 LLM 安全對齊
- [系統提示洩露](../knowledge/attacks/system-prompt-leakage.md) — OWASP 新增風險、ProxyPrompt 防禦
- [Unicode 隱形攻擊](../knowledge/attacks/unicode-invisible-attacks.md) — 變體選擇器、Glassworm 供應鏈攻擊
- [聯邦學習攻擊](../knowledge/attacks/federated-learning-attacks.md) — 投毒、推斷、後門攻擊
- [AI IDE 漏洞](../knowledge/attacks/ai-ide-vulnerabilities.md) — IDEsaster 24 CVE、秘密暴露、Rules File 後門

### 防禦策略 (`/knowledge/defenses/`)
- [Prompt Injection 防禦](../knowledge/defenses/prompt-injection-defense.md) — 多層防禦策略
- [沙箱與隔離](../knowledge/defenses/sandbox-isolation.md) — AI Agent 沙箱化技術與 Zero Trust
- [權限控制與審計](../knowledge/defenses/permission-audit.md) — RBAC、審計日誌、OWASP 權限風險
- [自動化決策治理](../knowledge/defenses/autonomous-decision-governance.md) — Agent 自主決策風險與治理框架
- [OWASP Agentic AI Top 10](../knowledge/defenses/owasp-agentic-top10.md) — ASI01-ASI10 完整風險清單與防禦
- [護欄與內容安全](../knowledge/defenses/guardrails-content-safety.md) — NeMo、Guardrails AI、Bedrock、Azure
- [AI-BOM 與供應鏈安全](../knowledge/defenses/ai-bom-supply-chain.md) — AI Bill of Materials、MLSecOps
- [水印與內容溯源](../knowledge/defenses/watermarking-provenance.md) — C2PA、隱寫術水印、模型指紋
- [多 Agent 安全架構](../knowledge/defenses/multi-agent-security.md) — A2A 協議、Service Mesh、Morris II 蠕蟲
- [事件回應](../knowledge/defenses/incident-response.md) — AI 特定 IR 框架、CoSAI、CISA Playbook
- [LLM 滲透測試](../knowledge/defenses/llm-pentesting-methodology.md) — OWASP AI Testing Guide、測試清單
- [隱私保護技術](../knowledge/defenses/privacy-preserving-llm.md) — 差分隱私、VaultGemma、DP-SGD
- [Zero Trust AI 架構](../knowledge/defenses/zero-trust-ai-architecture.md) — Microsoft 參考架構、分層防禦模式
- [EU AI Act 合規](../knowledge/defenses/eu-ai-act-compliance.md) — 2026-08 高風險 AI 義務、合規清單
- [MCP 安全防禦](../knowledge/defenses/mcp-security-guide.md) — OWASP MCP 指南、mcp-scan、防禦架構

### 工具與框架 (`/knowledge/tools/`)
- [Red Teaming 工具](../knowledge/tools/red-teaming-tools.md) — 紅隊測試工具與安全框架
- [防禦工具](../knowledge/tools/defense-tools.md) — Agent 治理、沙箱平台、安全掃描
- [可觀測性與監控](../knowledge/tools/observability-monitoring.md) — LLM 可觀測性平台、安全監控工具
