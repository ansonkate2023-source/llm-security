# LLM 不安全輸出處理（Insecure Output Handling）

**分類：** attack
**風險等級：** High
**最後更新：** 2026-04-06

## 概述

不安全輸出處理發生在 LLM 輸出未經適當驗證、清理或管理即傳遞至系統其他部分時。攻擊 LLM 整合類似於利用 SSRF 漏洞 — 濫用伺服器端系統對不可直接存取的元件發動攻擊。

## 漏洞類型

### 客戶端漏洞
- **XSS（跨站腳本）** — LLM 輸出包含惡意 JavaScript
- **CSRF（跨站請求偽造）** — LLM 輸出觸發未授權操作

### 伺服器端漏洞
- **SSRF（伺服器端請求偽造）** — LLM 被誘導向內部服務發送請求
- **遠端程式碼執行（RCE）** — LLM 輸出被直接執行
- **權限提升** — LLM 輸出繞過授權檢查

## 攻擊場景

### 場景 1：LLM → 資料庫
```
使用者輸入 → LLM 產生 SQL → 未清理直接執行 → SQL Injection
```

### 場景 2：LLM → Web 渲染
```
使用者輸入 → LLM 產生 HTML/JS → 未清理直接渲染 → XSS
```

### 場景 3：LLM → 內部 API
```
Prompt Injection → LLM 呼叫內部 API → 未驗證 → SSRF
```

### 場景 4：LLM → Shell 命令
```
使用者輸入 → LLM 產生命令 → 未清理直接執行 → RCE
```

## OWASP LLM02: Insecure Output Handling

OWASP 將此列為 LLM Top 10 第二大風險：
- LLM 輸出可能包含惡意內容
- 下游系統信任 LLM 輸出如同信任使用者輸入
- 缺乏輸出驗證等同於缺乏輸入驗證

## 防禦策略

### 核心原則
**永遠將 LLM 輸出視為不受信任的資料**

### 具體措施
1. **輸出驗證** — 對 LLM 輸出執行與使用者輸入相同的驗證
2. **編碼與轉義** — 在渲染前對 HTML/JS 內容進行編碼
3. **參數化查詢** — LLM 產生的 SQL 必須使用參數化查詢
4. **沙箱執行** — LLM 產生的程式碼在隔離環境中執行
5. **存取控制** — LLM 呼叫的 API 需獨立驗證權限
6. **內容安全策略** — 限制可執行的內容類型

## 參考

- [OWASP — Insecure Output Handling](https://genai.owasp.org/llmrisk2023-24/llm02-insecure-output-handling/)
- [PortSwigger — Web LLM Attacks](https://portswigger.net/web-security/llm-attacks)
- [SecureFlag — Improper Output Handling](https://knowledge-base.secureflag.com/vulnerabilities/code_injection/improper_output_handling_in_ai_llm_vulnerability.html)
- [Cobalt — LLM Insecure Output Handling](https://www.cobalt.io/blog/llm-insecure-output-handling)
