# AI Agent 安全攻擊

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

AI Agent 系統因具備資料檢索、工具呼叫、身份使用等能力，成為高價值攻擊目標。97% 企業預期一年內遭遇重大 AI Agent 安全事件，但僅 6% 安全預算投入此領域。

## 主要攻擊向量

### 1. Agent Commander（C2 攻擊）
- 透過 prompt injection 將 AI coding agent 轉換為持久性 C2 平台
- 自主 agent 成為遠端控制的惡意程式投遞系統
- 風險等級：Critical

### 2. 記憶/上下文操控
- Agent 可跨對話保留記憶，攻擊者可操控此記憶
- 被操控的記憶影響後續所有決策

### 3. 供應鏈攻擊
- 惡意 plugin/工具注入 agent 工作流程
- 單一被入侵元件可影響整個系統

### 4. 資料投毒
- 汙染訓練或微調資料
- 建立後門或引入偏見

### 5. 權限過度授予
- Agent 以真實身份與權限執行操作
- 邊界不清導致未授權操作

## 真實事件

### 墨西哥政府攻擊（2026-03）
- 攻擊者使用 AI agent 入侵十個墨西哥政府機構與一個金融機構
- 竊取超過 1 億人的資料

### AI 交易 Agent 漏洞（2026）
- $45M 加密貨幣安全漏洞，暴露 AI 交易 agent 的協議風險
- 來源：[KuCoin](https://www.kucoin.com/blog/en-ai-trading-agent-vulnerability-2026-how-a-45m-crypto-security-breach-exposed-protocol-risks)

## 企業現狀

- 80.9% 技術團隊已進入測試或生產
- 僅 14.4% agent 經完整安全與 IT 批准後上線
- 97% 企業預期一年內遭遇重大事件

## 防禦策略

- 最小權限原則
- 沙箱/隔離執行
- 工具使用審計
- 記憶完整性驗證
- 持續安全監控

## 參考

- [Zenity — AI Agent Threat Landscape 2026](https://zenity.io/resources/white-papers/2026-threat-landscape-report)
- [HBR — AI Agents Act Like Malware](https://hbr.org/2026/03/ai-agents-act-a-lot-like-malware-heres-how-to-contain-the-risks)
- [Security Boulevard — 97% Enterprises](https://securityboulevard.com/2026/04/97-of-enterprises-expect-a-major-ai-agent-security-incident-within-the-year/)
