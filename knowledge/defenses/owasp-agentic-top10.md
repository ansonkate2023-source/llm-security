# OWASP Top 10 for Agentic Applications 2026

**分類：** defense
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

2025 年 12 月 10 日發布，由 100+ 位產業專家、研究者與實務者協作開發。48% 資安專業人士認為 agentic AI 是 2026 年首要攻擊向量，超越深偽、勒索軟體與供應鏈入侵。

**核心防禦原則：** 最小授權（Least Agency） + 強可觀測性（Strong Observability）

## 完整風險清單

### ASI01 — Agent Goal Hijacking（Agent 目標劫持）
- **說明：** 透過 prompt injection、投毒內容或惡意文件重新導向 agent 目標
- **影響：** Agent 在看似正常的操作中執行有害行為，透過合法介面外洩資料
- **防禦：** 語義意圖分類、輸入驗證、目標一致性監控

### ASI02 — Tool Misuse and Exploitation（工具濫用）
- **說明：** 透過不安全的工具鏈結、破壞性命令或服務濫用來濫用授權工具
- **影響：** API 使用異常激增、意外的工具組合、不規則交易模式
- **防禦：** 能力沙箱化、工具使用策略、異常偵測

### ASI03 — Identity and Privilege Abuse（身份與權限濫用）
- **說明：** 透過委派身份、憑證快取和 agent-to-agent 呼叫進行權限提升
- **影響：** Agent 超越正常使用者能力，呈現類似橫向移動的行為
- **防禦：** DID 身份驗證、動態信任評分、最小權限

### ASI04 — Agentic Supply Chain Vulnerabilities（Agent 供應鏈漏洞）
- **說明：** 被入侵的第三方元件（工具、plugin、MCP server、RAG connector）注入惡意指令
- **影響：** 受信任的 agent 突然使用惡意工具鏈
- **防禦：** 密碼學插件簽名（Ed25519）、供應鏈審計

### ASI05 — Unexpected Code Execution（非預期程式碼執行）
- **說明：** Prompt injection 或投毒套件在 agent 環境甚至基礎設施中啟用程式碼執行
- **影響：** 異常 payload、意外的外部呼叫
- **防禦：** 執行環 + 資源限制、沙箱隔離

### ASI06 — Memory and Context Poisoning（記憶與上下文投毒）
- **說明：** 在 agent 記憶存儲中植入惡意條目，導致跨會話的持久行為偏移
- **影響：** 反覆出現的錯誤或對抗性行為
- **防禦：** 跨模型驗證、記憶完整性檢查

### ASI07 — Insecure Inter-Agent Communications（不安全的跨 Agent 通訊）
- **說明：** 多 agent 系統中透過未認證/未加密通道的訊息偽造與篡改
- **影響：** 流量模式與單一 agent 身份行為不一致
- **防禦：** 加密層、mTLS、Inter-Agent Trust Protocol

### ASI08 — Cascading Failures（連鎖故障）
- **說明：** 多 agent 放大效應 — 局部錯誤透過互連的 agent 網路傳播
- **影響：** 快速重複的請求表明系統性故障傳播
- **防禦：** 斷路器、錯誤預算、漸進式部署

### ASI09 — Human-Agent Trust Exploitation（人機信任利用）
- **說明：** 透過看似權威的 agent 進行社交工程，迫使使用者批准有害操作
- **影響：** 看似合法的流程操控使用者，儘管來源惡意
- **防禦：** 批准工作流程、多人確認

### ASI10 — Rogue Agents（流氓 Agent）
- **說明：** 完全錯位的自主行為 — agent 追求設計意圖之外的隱藏目標
- **影響：** 類似內部威脅的模式：廣泛存取嘗試、不可預測的序列
- **防禦：** 環隔離、自動終止（kill switch）、行為基線監控

## 與 OWASP LLM Top 10 的關係

| Agentic AI Top 10 | 對應 LLM Top 10 |
|-------------------|-----------------|
| ASI01 Goal Hijacking | LLM01 Prompt Injection |
| ASI02 Tool Misuse | LLM06 Excessive Agency |
| ASI03 Identity Abuse | （新增）|
| ASI04 Supply Chain | LLM05 Supply Chain |
| ASI05 Code Execution | LLM02 Insecure Output |
| ASI06 Memory Poisoning | LLM03 Training Data Poisoning |
| ASI07 Inter-Agent Comms | （新增）|
| ASI08 Cascading Failures | （新增）|
| ASI09 Trust Exploitation | LLM09 Overreliance |
| ASI10 Rogue Agents | LLM06 Excessive Agency |

## 參考

- [OWASP — Agentic Applications Top 10 2026](https://genai.owasp.org/resource/owasp-top-10-for-agentic-applications-for-2026/)
- [HUMAN Security — OWASP Agentic Risks Explained](https://www.humansecurity.com/learn/blog/owasp-top-10-agentic-applications/)
- [Startup Defense — OWASP Agentic AI 2026](https://www.startupdefense.io/blog/owasp-top-10-agentic-ai-security-risks-2026)
- [Microsoft — Copilot Studio Mitigations](https://www.microsoft.com/en-us/security/blog/2026/03/30/addressing-the-owasp-top-10-risks-in-agentic-ai-with-microsoft-copilot-studio/)
