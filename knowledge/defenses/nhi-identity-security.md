# 非人類身份安全（Non-Human Identity / NHI）

**分類：** defense
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

NHI（Non-Human Identities）包含服務帳號、API token、機器角色和 AI agent 憑證，數量已超過人類使用者 100:1，但仍處於 IAM 與審計審查範圍之外。AI agent 將 NHI 從靜態風險轉變為主動的自主操作者類別。任何不將 NHI 視為一等安全主體的 2026 策略都是結構性不健全的。

## 規模與現狀

| 指標 | 數據 |
|------|------|
| NHI 與人類使用者比例 | 100:1 |
| 有正式 AI 身份政策的組織 | < 25% |
| 不追蹤新 AI 身份建立的組織 | > 16% |
| GitGuardian NHI 安全融資 | $50M（2026-02）|

## 核心風險

### 1. 治理缺口
- NHI 處於 IAM 與審計審查範圍外
- 不到四分之一的組織有正式 AI 身份管理政策
- 超過 16% 組織不追蹤新 AI 身份的建立
- Token 和服務帳號在正式清單之外成長

### 2. 過度授權
- 企業給予 agent 廣泛權限，無問責、無可審計性、無有效控制
- AI agent 不同於服務帳號 — 動態選擇操作
- 比人類更可能在有機會時執行危險操作

### 3. 憑證生命週期
- AI agent 憑證缺乏有效的輪替與撤銷機制
- 長期存在的 token 成為攻擊目標
- 被入侵的 agent 憑證可影響整個系統

### 4. Shadow AI Agent
- 未經授權的 AI agent 使用自動建立 NHI
- 無法追蹤的身份增加攻擊面
- 結合 Shadow AI 問題更加嚴重

## NHI 類型與 AI Agent

| NHI 類型 | 說明 | AI 特有風險 |
|----------|------|-------------|
| 服務帳號 | 靜態存取 | 被 agent 動態呼叫時權限擴大 |
| API Token | API 存取憑證 | Agent 自動建立 token 不受控 |
| 機器角色 | 雲端資源角色 | Agent 可請求超出需要的角色 |
| Agent 憑證 | AI agent 專用身份 | 需要全新的管理模型 |
| MCP Server 身份 | 工具服務身份 | 工具投毒可利用身份 |

## 防禦策略

### NHI 生命週期管理
1. **盤點** — 完整清查所有 NHI（包含 AI agent 憑證）
2. **建立** — 正式流程建立 AI 身份，需批准
3. **權限** — 最小權限，動態調整
4. **監控** — 持續監控 NHI 行為
5. **輪替** — 定期輪替憑證
6. **撤銷** — 快速撤銷被入侵的身份

### Zero Trust 擴展
- 將 Zero Trust 原則延伸至非人類使用者
- 每次 agent 操作都需驗證
- 動態信任評分（非二元信任/不信任）

### 運行時約束
- AI agent 視為「有運行時約束的一等安全主體」
- 能力沙箱化
- 操作速率限制
- 異常行為偵測

## 安全工具供應商

| 供應商 | 焦點 |
|--------|------|
| **Astrix Security** | AI agent 與 NHI 身份安全 |
| **Entro Security** | Agentic AI 與 NHI 安全平台 |
| **GitGuardian** | NHI 安全（$50M 融資擴展 AI agent 安全）|
| **BeyondTrust** | 防止 Shadow AI 與 NHI 接管 |
| **Aembit** | NHI 生命週期管理（NHIcon 2026 主辦方）|

## CSA 調查報告

Cloud Security Alliance 發布 NHI 與 AI 安全調查報告，涵蓋：
- NHI 治理現狀
- AI agent 身份管理挑戰
- 產業最佳實務
- **來源：** [CSA](https://cloudsecurityalliance.org/artifacts/state-of-nhi-and-ai-security-survey-report)

## 參考

- [CSA — State of NHI and AI Security](https://cloudsecurityalliance.org/artifacts/state-of-nhi-and-ai-security-survey-report)
- [Astrix Security — AI Agent NHI](https://astrix.security/)
- [GitGuardian — $50M NHI Security](https://siliconangle.com/2026/02/11/gitguardian-raises-50m-expand-non-human-identity-ai-agent-security/)
- [BeyondTrust — Shadow AI and NHI](https://www.beyondtrust.com/blog/entry/preventing-shadow-ai-and-nhi-risk)
- [Cyber Strategy Institute — 2026 NHI Reality Report](https://cyberstrategyinstitute.com/2026-nhi-reality-report/)
- [MSSP Alert — Agentic AI and NHI 2026](https://www.msspalert.com/news/security-teams-mssps-will-wrestle-with-agentic-ai-non-human-identities-in-2026)
