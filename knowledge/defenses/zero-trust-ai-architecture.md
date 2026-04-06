# Zero Trust AI 安全架構

**分類：** defense
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

AI 系統不適用傳統安全模型，引入新的信任邊界：使用者與 agent 之間、模型與資料之間、人類與自動化決策之間。Microsoft 2026 年 3 月發布 Zero Trust for AI 參考架構。實施 Zero Trust + AI 的組織成功入侵減少 76%，同時降低營運成本。

## 三大核心原則

### 1. 明確驗證（Verify Explicitly）
- 持續評估 AI agent、工作負載與使用者的身份和行為
- 每次互動都需驗證
- 不假設任何先前的信任

### 2. 最小權限（Least Privilege）
- 限制對模型、prompt、plugin 和資料源的存取
- AI agent 僅獲得當前任務所需的能力
- 動態權限調整

### 3. 假設入侵（Assume Breach）
- 設計 AI 系統具備對 prompt injection、資料投毒、橫向移動的韌性
- 持續監控所有 AI 行為
- 偵測與回應能力

## Microsoft Zero Trust for AI 架構（2026-03）

### 核心元件
- 策略驅動的存取控制
- 持續驗證
- 監控與治理
- **Zero Trust Assessment for AI** — 2026 年夏季推出
- **來源：** [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/2026/03/19/new-tools-and-guidance-announcing-zero-trust-for-ai/)

## NVIDIA Confidential AI Factory

### 機密 AI 工廠架構
- 在整個 AI 生命週期中保護資料機密性
- 硬體級信任根（Hardware Root of Trust）
- 機密計算環境
- **來源：** [NVIDIA Developer Blog](https://developer.nvidia.com/blog/building-a-zero-trust-architecture-for-confidential-ai-factories/)

## AI Agent 作為非人類身份

### 新信任模型
- AI agent 需要自己的 Zero Trust 治理框架
- 被過度授權、被操控或錯位的 agent 如同「雙面間諜」
- 需要專門的身份管理（如 SPIFFE/DID）

### 產業應用
- **銀行** — 交易 agent 的權限控制
- **電信** — 網路管理 agent 的隔離
- **政府** — 決策 agent 的審計
- **來源：** [Medium — AI Agent Identity](https://medium.com/@raktims2210/ai-agent-identity-zero-trust-the-2026-playbook-for-securing-autonomous-systems-in-banks-e545d077fdff)

## 企業 AI 安全架構模式

### 分層防禦
```
┌─────────────────────────────────┐
│  使用者/外部介面層               │ ← 輸入驗證、認證
├─────────────────────────────────┤
│  AI 閘道/代理層                 │ ← 速率限制、護欄
├─────────────────────────────────┤
│  模型推理層                     │ ← 沙箱、最小權限
├─────────────────────────────────┤
│  資料/知識庫層                  │ ← 存取控制、加密
├─────────────────────────────────┤
│  工具/API 層                    │ ← 能力沙箱、審計
├─────────────────────────────────┤
│  監控/可觀測性層                │ ← 異常偵測、日誌
└─────────────────────────────────┘
```

### 關鍵控制點
1. **入口** — 輸入驗證、prompt injection 偵測
2. **模型** — 護欄、輸出過濾
3. **工具** — 能力限制、執行沙箱
4. **資料** — 存取控制、加密、溯源
5. **通訊** — Agent 間 mTLS、A2A 協議
6. **監控** — 全面可觀測性、告警

## 參考

- [Microsoft — Zero Trust for AI](https://www.microsoft.com/en-us/security/blog/2026/03/19/new-tools-and-guidance-announcing-zero-trust-for-ai/)
- [NVIDIA — Confidential AI Factory](https://developer.nvidia.com/blog/building-a-zero-trust-architecture-for-confidential-ai-factories/)
- [EC-Council — AI Security Architecture](https://www.eccouncil.org/cybersecurity-exchange/whitepaper/ai-security-architecture/)
- [Seceon — Zero Trust AI Security Guide 2026](https://seceon.com/zero-trust-ai-security-the-comprehensive-guide-to-next-generation-cybersecurity-in-2026/)
