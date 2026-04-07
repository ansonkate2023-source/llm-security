# Prompt Injection 防禦策略

**分類：** defense
**風險等級：** Critical
**最後更新：** 2026-04-07

## 概述

針對 2026 年激增的 prompt injection 攻擊（增長 340%），以下整理當前最佳防禦實務。

## 防禦層級

### 1. 輸入層
- **輸入驗證與清理** — 過濾已知攻擊模式
- **使用者輸入與系統提示分離** — 明確區分不同來源的文字
- **內容安全策略** — 限制可處理的內容類型

### 2. 模型層
- **多層安全護欄** — 不依賴單一防線
- **指令階層** — 建立明確的指令優先順序
- **輸出過濾** — 檢測並阻擋異常輸出

### 3. 系統層
- **最小權限原則** — AI 系統僅授予必要權限
- **沙箱隔離** — 在受限環境中執行 AI 操作
- **audit trail** — 記錄所有 AI 操作以供審計

### 4. 監控層
- **異常偵測** — 監控 AI 行為模式變化
- **RLM-JB 偵測框架** — 專門針對 jailbreak 的偵測方法
- **持續紅隊測試** — 定期測試防禦有效性

## OWASP 建議

根據 OWASP LLM Top 10，prompt injection 防禦應包含：
- 輸入/輸出過濾
- 權限控制
- 人工介入機制（human-in-the-loop）
- 外部內容標記

## Microsoft Copilot Studio 防禦措施

Microsoft 已在 Copilot Studio 中實作 OWASP Agentic AI Top 10 的對應防禦，可作為企業參考。

## 新型防禦技術（2026-04 更新）

### DefensiveTokens（ACM AISec 2026）
- 在 LLM 輸入前插入安全性優化的特殊 token，無需重新訓練模型
- 31K+ 樣本基準測試：手動 prompt injection 攻擊成功率降至 0.24%
- 來源：[ACM Digital Library](https://dl.acm.org/doi/10.1145/3733799.3762982)

### SafeProbing — 解碼時安全意識探測（arXiv 2026）
- 核心觀察：LLM 被攻擊生成有害內容時保留潛在安全意識，但因連貫性需求被壓制
- 在解碼過程中即時探測安全意識信號，在有害內容生成時偵測並干預
- 來源：[arXiv:2601.10543](https://arxiv.org/abs/2601.10543)

### OpenAI Atlas 自動紅隊
- RL 訓練的 LLM 作為自動攻擊者，發現多步驟 prompt injection
- OpenAI 坦承 prompt injection「不太可能被完全解決」
- 來源：[OpenAI](https://openai.com/index/hardening-atlas-against-prompt-injection/)

### CCA 防禦建議
- 伺服器端對話歷史維護（不信任客戶端歷史）
- 對話記錄數位簽章
- 來源：[Microsoft MSRC](https://msrc.microsoft.com/blog/2025/03/jailbreaking-is-mostly-simpler-than-you-think/)

## 參考

- [OWASP LLM01 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- [Microsoft — OWASP Agentic AI](https://www.microsoft.com/en-us/security/blog/2026/03/30/addressing-the-owasp-top-10-risks-in-agentic-ai-with-microsoft-copilot-studio/)
- [Silverfort — RLM-JB](https://www.silverfort.com/blog/rlm-jb-a-new-approach-to-ai-jailbreak-detection/)
- [ACM — DefensiveTokens](https://dl.acm.org/doi/10.1145/3733799.3762982)
- [arXiv — SafeProbing](https://arxiv.org/abs/2601.10543)
- [OpenAI — Hardening Atlas](https://openai.com/index/hardening-atlas-against-prompt-injection/)
