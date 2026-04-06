# AI 權限控制與審計

**分類：** defense
**風險等級：** High
**最後更新：** 2026-04-06

## 概述

隨著 AI agent 獲得越來越多的自主權，權限控制與審計日誌成為企業 AI 安全的基石。OWASP 將過度授權（Excessive Agency）列為 LLM 安全重要風險。

## 權限控制框架

### 最小權限原則
- LLM 僅授予每個角色所需的最低權限
- 應用 RBAC（角色基礎存取控制）
- 實施 MFA 與上下文存取檢查
- 跨 prompt、plugin、檢索路徑實施權限控制

### 有效權限模型
有效權限應為以下三者的交集：
1. **LLM 權限** — 模型本身的能力限制
2. **使用者權限** — 使用者的授權範圍
3. **任務權限** — 特定任務所需的權限

### 人工驗證
- 高影響操作必須要求人工驗證（Human-in-the-Loop）
- 建立批准工作流程

## 審計日誌要求

### 必須記錄的項目
- Prompt 歷史
- 模型決策
- 輸出修改
- 護欄執行
- 檢索步驟（RAG 流程）
- 管理員操作

### 日誌安全要求
- 加密存儲
- 存取限制
- 依法規時限保存
- 防竄改機制

### 隱私安全日誌實務（SOC 2 / HIPAA）
- 欄位許可列表
- 持久化前的資料遮罩
- 假名化 ID
- 僅引用的檢索追蹤
- 緊急存取機制（break-glass）
- 保留控制

## OWASP LLM Top 10 2025 — 權限相關風險

### LLM06: Excessive Agency（過度授權）
- AI 系統執行超出預期範圍的操作
- 防禦：外部授權層、有效權限交集、人工驗證

### LLM07: System Prompt Leakage（新增）
- 系統提示包含敏感指令、憑證或操作邏輯
- 防禦：不在 system prompt 中存放機密

### LLM10: Unbounded Consumption（原 DoS）
- 擴展為包含資源管理與意外營運成本風險
- 防禦：資源配額、使用監控

## ZombieAgent 攻擊
- 2026 年初研究展示間接 prompt injection 可在連接的 agent 間持久化
- 影響所有跨 agent 通訊的系統
- 防禦需要跨 agent 的信任驗證

## 參考

- [OWASP LLM Top 10 2025](https://genai.owasp.org/llm-top-10/)
- [Lasso Security — LLM Compliance](https://www.lasso.security/blog/llm-compliance)
- [MintMCP — AI Agent Security Audit](https://www.mintmcp.com/blog/ai-agent-security-audit)
- [Newline — Audit Logs for LLM Pipelines](https://www.newline.co/@zaoyang/audit-logs-for-llm-pipelines-key-practices--a08f2c2d)
- [OptyxStack — LLM Logging Without PII](https://optyxstack.com/security-compliance/llm-logging-without-pii-observability-patterns)
