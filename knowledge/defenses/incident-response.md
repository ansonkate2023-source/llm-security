# AI 安全事件回應（Incident Response）

**分類：** defense
**風險等級：** High
**最後更新：** 2026-04-06

## 概述

AI 安全事件從 2023 至 2024 年激增 56.4%，達 233 起記錄案例。然而大多數組織缺乏 AI 特定的事件回應程序。67% 的 AI 事件源自模型錯誤而非對抗性攻擊，但組織不成比例地投入外部威脅防禦。AI 事件平均需 4.5 天才能偵測。

## 六階段回應框架（NIST SP 800-61）

### Phase 1: 準備（Preparation）
- 建立監控、Runbook 與團隊能力
- 組建 CSIRT（最少需要：執行贊助人、事件指揮官）
- 集中遙測（SIEM/XDR）+ 不可變備份
- 建立嚴重性分級與帶外通訊

### Phase 2: 偵測（Detection）
- 跨人口群的效能監控
- 使用統計測試的漂移偵測
- 異常預測模式偵測
- 輸出驗證與事實查核
- 使用者投訴通道

### Phase 3: 遏制（Containment）
- 流量節流至完全關閉的選項
- 基於嚴重性與事件類型決策
- 保留鑑識證據

### Phase 4: 根除（Eradication）
- 重新訓練模型
- 資料清理
- 系統修補

### Phase 5: 復原（Recovery）
- 驗證修復
- 漸進恢復營運
- 持續監控

### Phase 6: 經驗學習（Lessons Learned）
- 記錄發現
- 防止再發
- 更新 Playbook

## AI 特有挑戰

傳統 IT 事件回應無法涵蓋的 AI 故障模式：

| 故障類型 | 說明 | 偵測難度 |
|----------|------|----------|
| 模型漂移 | 輸入/概念分佈偏移導致效能退化 | 中 |
| 對抗性攻擊 | 故意輸入操控導致錯誤分類 | 高 |
| 資料投毒 | 被汙染的訓練資料引入後門 | 極高 |
| 偏見事件 | 對受保護群體的系統性不公平 | 中 |
| 幻覺 | 生成式 AI 產生虛假輸出 | 中 |
| 隱私洩露 | 透過模型輸出的意外曝露 | 高 |

## CoSAI AI 事件回應框架

Coalition for Secure AI（CoSAI）發布 v1.0 框架：
- 使用 OASIS CACAO 標準撰寫 Playbook
- 針對特定 AI 攻擊的詳細可操作工作流程
- 包含偵測方法、分類標準、遏制步驟、復原程序
- **來源：** [CoSAI](https://www.coalitionforsecureai.org/defending-ai-systems-a-new-framework-for-incident-response-in-the-age-of-intelligent-technology/)

## CISA AI 網路安全協作 Playbook

美國 CISA 發布 AI 網路安全協作 Playbook：
- 政府與產業界的 AI 安全協作指引
- **來源：** [CISA](https://www.cisa.gov/resources-tools/resources/ai-cybersecurity-collaboration-playbook)

## AI 事件鑑識工具

- **SHAP 分析** — 解釋模型決策
- **訓練資料檢查** — 尋找投毒跡象
- **MITRE ATLAS 映射** — 對抗性事件分類
- **漂移偵測** — 統計測試識別分佈偏移

## 未來趨勢

IDC 預測：至 2027 上半年，85% 的偵測與回應 Playbook 將在 SOC 告警觸發時動態生成。

## 參考

- [GLACIS — AI Incident Response Playbook](https://www.glacis.io/guide-ai-incident-response)
- [CoSAI — AI IR Framework v1.0](https://www.coalitionforsecureai.org/defending-ai-systems-a-new-framework-for-incident-response-in-the-age-of-intelligent-technology/)
- [CISA — AI Cybersecurity Collaboration Playbook](https://www.cisa.gov/resources-tools/resources/ai-cybersecurity-collaboration-playbook)
- [Microsoft — Detecting Prompt Abuse](https://www.microsoft.com/en-us/security/blog/2026/03/12/detecting-analyzing-prompt-abuse-in-ai-tools/)
- [MDPI — Practical IR Framework for GenAI](https://www.mdpi.com/2624-800X/6/1/20)
