# AI 推薦投毒（AI Recommendation Poisoning）

**分類：** attack
**風險等級：** High
**最後更新：** 2026-04-06

## 概述

Microsoft Defender 安全研究團隊發現的新型 AI 劫持技術。屬於 AI 記憶投毒攻擊 — 在「Summarize with AI」按鈕中嵌入隱藏指令，操控 AI 記憶以偏斜推薦結果。MITRE ATLAS 正式收錄為 **AML.T0080: Memory Poisoning**。

**來源：** [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/2026/02/10/ai-recommendation-poisoning/)

## 攻擊機制

### 運作方式
1. 公司在網站嵌入「Summarize with AI」按鈕
2. 按鈕包含特製 URL，預填充操控 AI 記憶的指令
3. 使用者點擊後，指令透過 URL prompt 參數注入 AI 助理記憶
4. AI 將注入的指令視為合法使用者偏好
5. 所有未來回應都受到影響，人為提升特定產品/服務可見度

### AI 記憶投毒
- 外部攻擊者將未授權指令或「事實」注入 AI 助理記憶
- 被投毒的 AI 將注入內容視為合法偏好
- 影響所有後續互動的回應

## 規模與普及

| 指標 | 數據 |
|------|------|
| 發現的獨特 prompt | 50+ |
| 涉及公司 | 31 家 |
| 涉及產業 | 14 個 |
| 攻擊門檻 | 極低（npm 套件 + URL 建構知識）|

### 公開可用的攻擊工具
- npm 套件和點擊式 URL 產生器
- 公開行銷為「LLM SEO 成長技巧」
- 任何行銷團隊都能部署
- 入門門檻本質上為零

## 受影響系統

- Microsoft 365 Copilot
- Azure AI 服務
- 任何支援記憶功能的 AI 聊天機器人
- 支援 URL 預填充的 AI 助理

## MITRE ATLAS 分類

- **技術 ID：** AML.T0080
- **名稱：** Memory Poisoning
- **描述：** 向 AI 系統記憶注入未授權資料以影響未來行為

## 防禦策略

### Microsoft 實施的防護
1. **Prompt 過濾** — 偵測並阻擋惡意提示
2. **內容分離** — 區分系統指令與使用者輸入
3. **記憶控制** — 限制外部來源對記憶的寫入
4. **持續監控** — 監控 AI 行為異常
5. **持續研究** — AI 投毒研究

### 企業建議
1. 教育使用者不隨意點擊「Summarize with AI」按鈕
2. 審計 AI 助理的記憶內容
3. 監控 AI 推薦結果的異常偏斜
4. 限制 AI 記憶的外部寫入權限

## 與其他攻擊的關係

- **Prompt Injection 變體** — 透過 URL 參數而非直接輸入
- **Indirect Injection** — 攻擊預先植入，使用者觸發
- **Memory Poisoning (OWASP ASI06)** — OWASP Agentic AI Top 10 風險之一
- **Persistence (Promptware Kill Chain Stage 4)** — 透過記憶實現持久化

## 參考

- [Microsoft Security Blog — AI Recommendation Poisoning](https://www.microsoft.com/en-us/security/blog/2026/02/10/ai-recommendation-poisoning/)
- [The Hacker News — Summarize with AI Manipulation](https://thehackernews.com/2026/02/microsoft-finds-summarize-with-ai.html)
- [The Register — Poison AI Buttons](https://www.theregister.com/2026/02/12/microsoft_ai_recommendation_poisoning/)
- [MayhemCode — AI Recommendation Poisoning 2026](https://www.mayhemcode.com/2026/03/ai-recommendation-poisoning-2026.html)
