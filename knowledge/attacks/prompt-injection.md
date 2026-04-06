# Prompt Injection 攻擊

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

Prompt injection 是 OWASP LLM Top 10 排名第一的漏洞類別。2026 年攻擊量激增 340%，67% 的成功攻擊在企業環境中超過 72 小時未被偵測。

## 攻擊類型

### 直接注入（Direct Injection）
攻擊者在使用者輸入中直接嵌入惡意指令，覆寫系統提示或改變模型行為。

### 間接注入（Indirect Injection）
攻擊者將惡意指令預先嵌入 AI 系統稍後會處理的內容中（如網頁、文件、資料庫），AI 在處理時自動觸發。

### 多模態注入（Multimodal Injection）
在圖像中嵌入視覺化對抗指令，利用多模態 AI 的跨模態互動漏洞。

## 攻擊向量

1. **使用者輸入** — 直接在對話中注入
2. **RAG 資料源** — 汙染檢索資料
3. **工具描述** — MCP tool poisoning
4. **圖像/文件** — 多模態攻擊
5. **電子郵件/網頁** — 間接注入

## 影響範圍

- 所有 LLM 應用
- AI Agent 系統
- RAG 系統
- 多模態 AI 系統

## 防禦策略

1. 輸入/輸出過濾與清理
2. 系統提示與使用者輸入分離
3. 最小權限原則
4. 內容安全策略
5. 監控與異常偵測

## 參考

- [OWASP LLM01:2025 Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/)
- [Sombra Inc — LLM Security Risks 2026](https://sombrainc.com/blog/llm-security-risks-2026)
