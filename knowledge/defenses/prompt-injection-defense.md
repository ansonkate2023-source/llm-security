# Prompt Injection 防禦策略

**分類：** defense
**風險等級：** Critical
**最後更新：** 2026-04-06

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

## 參考

- [OWASP LLM01 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- [Microsoft — OWASP Agentic AI](https://www.microsoft.com/en-us/security/blog/2026/03/30/addressing-the-owasp-top-10-risks-in-agentic-ai-with-microsoft-copilot-studio/)
- [Silverfort — RLM-JB](https://www.silverfort.com/blog/rlm-jb-a-new-approach-to-ai-jailbreak-detection/)
