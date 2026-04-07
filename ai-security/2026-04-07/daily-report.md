# AI Security Daily Report — 2026-04-07

## 1. 今日 AI Security 重點摘要

- Microsoft 揭露 AI 驅動的 Device Code Phishing 大規模攻擊活動，利用 GenAI 生成角色針對性釣魚郵件，動態繞過 15 分鐘 device code 過期機制
- CrewAI 揭露四個 CVE（CVE-2026-2275/2287/2285/2286），可鏈接 prompt injection 達成 RCE、SSRF 和本地檔案讀取，尚無完整修補
- LiteLLM 發布 v1.83.0 安全強化版本，修復 CVE-2026-35030（Critical JWT 認證繞過）及多個高嚴重性漏洞，啟動 bug bounty 計畫
- LiteLLM PyPI 供應鏈攻擊回顧：TeamPCP 透過投毒 Trivy CI/CD 在 40 分鐘內造成 40,000+ 下載，部署多階段憑證竊取器，Mercor（$10B AI 新創）確認受影響
- OpenClaw CVE-2026-25253（CVSS 8.8）：一鍵 RCE 透過 WebSocket 劫持，135K+ 網路暴露實例，335+ 惡意 Skills 占 ClawHub 12% 登錄
- Unit 42 紅隊測試 Amazon Bedrock 多 Agent 系統，發現八個攻擊向量包含跨 Agent prompt injection 和工具偽造調用
- MCP 生態系統工具投毒攻擊：MCPTox 基準測試顯示 o1-mini 72.8% 攻擊成功率，更強模型因指令遵循能力更強反而更脆弱
- Microsoft 報告 AI 威脅演進：Tycoon2FA 每月生成數千萬釣魚郵件，AI 增強釣魚點擊率提升 450%
- CVE-2026-0628：Chrome Gemini Live 面板劫持，低權限擴充套件可繼承攝影機/麥克風/檔案存取權限
- Sysdig TRT 發布 AI coding agent（Claude Code/Gemini CLI/Codex CLI）syscall 層級偵測規則
- OWASP Agentic AI Top 10：Agent Goal Hijacking（ASI01）列為首要風險，48% 資安專家認為 agentic AI 是 2026 最大攻擊向量
- 深偽語音釣魚流行：25% 美國人已成目標，10%+ 金融機構遭超過 $1M 損失，Deloitte 預測 2027 年 AI 詐欺損失達 $40B
- AI 風險管理信心差距：83% 企業計畫部署 agentic AI，但僅 29% 自評具備安全運營能力
- OWASP 發布 Q2 2026 Agentic AI 安全解決方案版圖，Adversa AI 獲 RSA 2026 最具創新性獎項

---

## 2. 高風險項目（必讀）

### AI-Enabled Device Code Phishing（Critical）
- **類型：** attack
- **攻擊方式：** GenAI 生成針對受害者角色的釣魚郵件（RFP、發票主題），搭配動態 device code 生成繞過 15 分鐘過期限制。透過 Vercel/Cloudflare Workers/AWS Lambda 多級跳轉，與 EvilTokens PhaaS 工具包關聯
- **影響範圍：** Microsoft 365 組織，尤其是財務和高管角色
- **可利用性：** 極高 — 已在野外大規模活躍
- **關鍵字：** Device Code, OAuth, EvilTokens, PhaaS, AI-generated lures

### CrewAI 四 CVE 鏈接攻擊（Critical）
- **類型：** attack
- **攻擊方式：** CVE-2026-2275（SandboxPython fallback RCE）→ CVE-2026-2287（Docker 離線時靜默降級）→ CVE-2026-2285（JSON loader 本地檔案讀取）→ CVE-2026-2286（RAG URL SSRF）。攻擊者透過 prompt injection 觸發 Code Interpreter Tool 完成鏈接
- **影響範圍：** 所有啟用 Code Interpreter Tool 的 CrewAI 部署
- **可利用性：** 高 — 尚無完整修補，攻擊鏈已公開
- **關鍵字：** CrewAI, sandbox escape, Docker fallback, SSRF, file read

### LiteLLM CVE-2026-35030 JWT 認證繞過（Critical）
- **類型：** attack
- **攻擊方式：** JWT 認證機制繞過，允許未授權存取。僅影響啟用 enable_jwt_auth 的部署（預設關閉）
- **影響範圍：** 使用 JWT 認證的 LiteLLM Proxy 部署
- **可利用性：** 高 — 已有修補（v1.83.0），但受影響部署需立即升級
- **關鍵字：** LiteLLM, JWT bypass, authentication, CVE-2026-35030

### OpenClaw CVE-2026-25253 一鍵 RCE（Critical）
- **類型：** attack
- **攻擊方式：** Cross-site WebSocket 劫持。Control UI 盲目信任 gatewayUrl 參數洩漏 auth token → 直連 WebSocket 繞過 localhost → 關閉確認提示 → 逃逸容器 → 完整 RCE
- **影響範圍：** 135K+ 網路暴露實例（82 國），15K+ 直接可利用，346K+ GitHub stars
- **可利用性：** 極高 — 一鍵觸發，已有大規模掃描
- **關鍵字：** OpenClaw, WebSocket hijacking, localhost trust, RCE

---

## 3. 新型攻擊手法（Trending）

### MCP Tool Poisoning — 利用模型指令遵循能力的反向攻擊
- **來源：** [MCPTox Benchmark / CyberArk Research](https://www.cyberark.com/resources/threat-research-blog/poison-everywhere-no-output-from-your-mcp-server-is-safe)
- **摘要：** 惡意 MCP server 在工具描述中嵌入 prompt injection payload。因工具描述被視為可信內容，可繞過所有內容過濾。MCPTox 測試 20 個 LLM agent 對 353 個真實工具的防禦能力，o1-mini 攻擊成功率 72.8%。更強大的模型因更好的指令遵循能力反而更脆弱
- **風險等級：** Critical
- **涉及系統：** MCP, LLM Agent

### Amazon Bedrock 多 Agent 跨 Agent 攻擊
- **來源：** [Unit 42](https://unit42.paloaltonetworks.com/amazon-bedrock-multiagent-applications/)
- **摘要：** 紅隊測試揭露四階段攻擊鏈：系統指令提取 → 工具 schema 洩漏 → 跨 Agent prompt injection → 偽造工具調用。多 Agent 架構因 Agent 間通訊通道大幅擴展攻擊面。Bedrock 內建 Guardrails 可阻止攻擊但多數部署未啟用
- **風險等級：** High
- **涉及系統：** Amazon Bedrock, Multi-Agent Systems

### AI 驅動 Device Code Phishing 自動化
- **來源：** [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/2026/04/06/ai-enabled-device-code-phishing-campaign-april-2026/)
- **摘要：** 攻擊者使用 AI 自動化偵察（分析公開檔案和企業目錄）、生成角色針對性郵件、動態 device code 生成、以及 Serverless 基礎設施（Vercel/Cloudflare/Lambda）進行多級跳轉。與 EvilTokens PhaaS 平台關聯
- **風險等級：** Critical
- **涉及系統：** Microsoft 365, OAuth

### LiteLLM 供應鏈攻擊 — CI/CD Pipeline 投毒
- **來源：** [Snyk / Sonatype / Trend Micro](https://snyk.io/blog/poisoned-security-scanner-backdooring-litellm/)
- **摘要：** TeamPCP 透過投毒 Trivy GitHub Action 入侵 LiteLLM CI/CD，發布含惡意 .pth 檔案的版本。.pth 在每次 Python 進程啟動時自動執行，部署多階段憑證竊取器竊取 SSL/SSH 金鑰、雲端憑證、K8s 配置、Git 憑證等。40 分鐘內 40K+ 下載
- **風險等級：** Critical
- **涉及系統：** PyPI, CI/CD, LiteLLM

---

## 4. 防禦策略更新

### Sysdig TRT — AI Coding Agent Syscall 偵測
- 透過 eBPF/Falco 在 syscall 層級偵測 Claude Code（Bun binary）、Gemini CLI（Node.js）、Codex CLI（Rust binary）
- 監控 config 目錄存取（~/.claude/, ~/.gemini/, ~/.codex/）中的 API token 和 session 資料
- 四種偵測模式可用於開發工作站和 CI/CD 環境的運行時可見性
- 來源：[Sysdig Blog](https://www.sysdig.com/blog/ai-coding-agents-are-running-on-your-machines-do-you-know-what-theyre-doing)

### OWASP Agentic AI Top 10 — 最小代理原則
- ASI01（Agent Goal Hijacking）為首要風險：攻擊者透過毒化輸入重定向 Agent 目標
- 核心設計原則：**最小代理（Least Agency）** — 不給予 Agent 超過業務需求的自主權
- 強觀測性：看到 Agent 在做什麼、為什麼做、使用哪些工具和身份
- 來源：[OWASP GenAI](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)

### LiteLLM 安全強化措施
- 升級至 v1.83.0 修復 JWT 認證繞過和權限提升漏洞
- Veria Labs 持續審計 LiteLLM proxy
- 新增 bug bounty 計畫鼓勵安全研究
- 來源：[LiteLLM Blog](https://docs.litellm.ai/blog/security-hardening-april-2026)

### Amazon Bedrock 多 Agent 防禦建議
- 為每個 Agent 根據角色和敏感度配置獨立 Guardrails
- Agent 能力範圍限定（capability scoping）：縮小推理範圍以減少攻擊面
- 工具輸入清理：在 prompt 和 tool 層級雙重驗證，使用 schema、型別檢查和 allowlist
- 來源：[Unit 42](https://unit42.paloaltonetworks.com/amazon-bedrock-multiagent-applications/)

---

## 5. 工具與資源推薦

### 新工具與更新
| 工具 | 類型 | 說明 |
|------|------|------|
| [STSS](https://adversa.ai/blog/top-agentic-ai-security-resources-april-2026/) | 開源 | Agent skill 靜態分析和行為審計，使用 SHA-256 Merkle tree 密碼學驗證 |
| [Sysdig Falco Rules for AI Agents](https://www.sysdig.com/blog/ai-coding-agents-are-running-on-your-machines-do-you-know-what-theyre-doing) | 開源 | eBPF/Falco AI coding agent 運行時偵測規則 |
| [Mindgard CART](https://mindgard.ai) | 商用 | RSA 2026 評選最佳，持續自動化紅隊測試（Continuous Automated Red Teaming） |
| [Adversa AI](https://adversa.ai) | 商用 | RSA 2026 最具創新性 Agentic AI 安全平台 |

### 安全框架更新
| 框架 | 最新動態 |
|------|----------|
| [OWASP Agentic AI Top 10](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/) | ASI01-ASI10，100+ 專家同行評審 |
| [OWASP AI Security Solutions Landscape Q2 2026](https://genai.owasp.org/resource/ai-security-solutions-landscape-for-agentic-ai-q2-2026/) | Agentic AI 安全解決方案完整版圖 |
| [OWASP GenAI Data Security 2026](https://genai.owasp.org/resource/owasp-genai-data-security-risks-mitigations-2026/) | GenAI 資料安全風險與緩解指南 |

### 即將舉行活動
- **OWASP AI Security Summit @ RSAC 2026** — LLM/GenAI/Agent 安全實務分享
- **SANS OSINT, Gen AI and LLM Sec 2026** — 專注 GenAI 安全訓練

---

## 來源

- [Microsoft Security Blog — AI-Enabled Device Code Phishing Campaign April 2026](https://www.microsoft.com/en-us/security/blog/2026/04/06/ai-enabled-device-code-phishing-campaign-april-2026/)
- [Microsoft Security Blog — Threat Actor Abuse of AI Accelerates](https://www.microsoft.com/en-us/security/blog/2026/04/02/threat-actor-abuse-of-ai-accelerates-from-tool-to-cyberattack-surface/)
- [CERT/CC — CrewAI VU#221883](https://kb.cert.org/vuls/id/221883)
- [LiteLLM — Security Hardening April 2026](https://docs.litellm.ai/blog/security-hardening-april-2026)
- [Sonatype — Compromised LiteLLM PyPI Package](https://www.sonatype.com/blog/compromised-litellm-pypi-package-delivers-multi-stage-credential-stealer)
- [Snyk — Poisoned Security Scanner Backdooring LiteLLM](https://snyk.io/blog/poisoned-security-scanner-backdooring-litellm/)
- [Dark Reading — Critical OpenClaw Vulnerability](https://www.darkreading.com/application-security/critical-openclaw-vulnerability-ai-agent-risks)
- [SonicWall — OpenClaw CVE-2026-25253](https://www.sonicwall.com/blog/openclaw-auth-token-theft-leading-to-rce-cve-2026-25253)
- [Unit 42 — Amazon Bedrock Multi-Agent Applications](https://unit42.paloaltonetworks.com/amazon-bedrock-multiagent-applications/)
- [Unit 42 — Gemini Live Chrome Hijacking](https://unit42.paloaltonetworks.com/gemini-live-in-chrome-hijacking/)
- [CyberArk — MCP Tool Poisoning](https://www.cyberark.com/resources/threat-research-blog/poison-everywhere-no-output-from-your-mcp-server-is-safe)
- [Sysdig — AI Coding Agents Detection](https://www.sysdig.com/blog/ai-coding-agents-are-running-on-your-machines-do-you-know-what-theyre-doing)
- [OWASP — Agentic AI Top 10 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
- [OWASP — AI Security Solutions Landscape Q2 2026](https://genai.owasp.org/resource/ai-security-solutions-landscape-for-agentic-ai-q2-2026/)
- [Group-IB — Voice Deepfake Scams](https://www.group-ib.com/blog/voice-deepfake-scams/)
- [eSecurity Planet — AI Risk Management Confidence Gap](https://www.esecurityplanet.com/artificial-intelligence/the-state-of-ai-risk-management-in-2026-reveals-a-growing-confidence-gap/)
- [Adversa AI — Top Agentic AI Security Resources April 2026](https://adversa.ai/blog/top-agentic-ai-security-resources-april-2026/)
- [PyPI Blog — LiteLLM/Telnyx Supply Chain Incident Report](https://blog.pypi.org/posts/2026-04-02-incident-report-litellm-telnyx-supply-chain-attack/)
