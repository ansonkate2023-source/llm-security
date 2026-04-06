# 多 Agent 安全架構與 A2A 協議

**分類：** defense
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

Agent2Agent Protocol（A2A）是 Google 於 2025 年 4 月推出的開放標準，2026 年由 Linux Foundation 正式接管。提供跨框架、跨供應商、跨域的 AI agent 安全協作標準。28% 企業高管將 AI agent 信任不足列為前三大挑戰。

## A2A 協議安全架構

### 核心安全功能

| 層級 | 機制 | 說明 |
|------|------|------|
| 通訊加密 | HTTPS/mTLS | 所有通訊加密，確保機密性、完整性、真實性 |
| 身份驗證 | SPIFFE + Token | 為每個 agent 建立非人類身份 |
| 存取控制 | 策略框架 | 與企業策略框架相容的存取控制 |
| 信任管理 | PKI/簽名 | 跨組織信任透過 PKI 簽名建立 |
| 審計 | 標準元資料 | 標準化元資料支援審計 |

### 跨組織安全
- 多租戶、跨域設計
- Company A 的 agent 可委派給 Company B 的 agent
- 前提：雙方信任彼此的 PKI/簽名
- 關鍵差異：超越單租戶解決方案

## 多 Agent 安全風險

### A2A 協議安全分析識別的風險
1. **偽造（Spoofing）** — agent 身份偽冒
2. **任務重放（Task Replay）** — 重放先前的任務請求
3. **權限提升** — 透過 agent-to-agent 呼叫提升權限
4. **Prompt Injection** — 透過 agent 通訊注入惡意指令

### 安全增強措施
- 密碼學控制
- Schema 強制
- 安全會話處理
- 細粒度授權

## Service Mesh 安全模型

### 架構
```
Agent A → [mTLS] → Service Mesh → [mTLS] → Agent B
              ↑                         ↑
         SPIFFE ID                 SPIFFE ID
         Policy enforcement        Policy enforcement
```

### 關鍵元件
- **Service Mesh** — 透過 mTLS 加密保護 agent 間通訊
- **SPIFFE** — 為每個 agent 建立非人類身份的認證協議
- **加密通道** — 防止能力協商與握手協議被攔截

## AI 蠕蟲威脅

### Morris II — 首個 AI 蠕蟲
- 透過對抗性自我複製 prompt 攻擊 GenAI 生態系統
- 利用 RAG 被動存儲並以零點擊方式傳播
- 已在 Gemini Pro、ChatGPT 4.0、LLaVA 上測試
- 能力：敏感資料萃取、垃圾郵件傳播
- 尚未在野外出現，但概念已驗證
- **來源：** [arXiv](https://arxiv.org/abs/2403.02817) / [IBM](https://www.ibm.com/think/insights/morris-ii-self-replicating-malware-genai-email-assistants)

### 對多 Agent 系統的影響
- 蠕蟲可在互連的 agent 生態系統中自我傳播
- 單一感染的 agent 可汙染所有連接的 agent
- 需要嚴格的 agent 間通訊隔離與驗證

## 防禦策略

### Zero Trust for AI Agents
1. **明確驗證** — 每次 agent 互動都驗證
2. **最小權限** — agent 僅獲得必要能力
3. **假設入侵** — 持續監控所有 agent 行為

### 實施建議
1. 所有 agent 通訊使用 mTLS
2. 為每個 agent 建立唯一身份（SPIFFE）
3. 實施細粒度授權策略
4. 監控 agent 間流量模式
5. 部署斷路器防止連鎖故障
6. 定期審計 agent 行為日誌

## 參考

- [A2A Protocol](https://a2a-protocol.org/latest/)
- [IBM — Agent2Agent Protocol](https://www.ibm.com/think/topics/agent2agent-protocol)
- [Linux Foundation — A2A Protocol Project](https://www.linuxfoundation.org/press/linux-foundation-launches-the-agent2agent-protocol-project-to-enable-secure-intelligent-communication-between-ai-agents)
- [Elevate Consult — Zero Trust AI Agents 2026](https://elevateconsult.com/insights/securing-autonomous-ai-agents-in-2026-what-every-business-needs-to-know/)
- [arXiv — Building Secure A2A Application](https://arxiv.org/html/2504.16902v2)
