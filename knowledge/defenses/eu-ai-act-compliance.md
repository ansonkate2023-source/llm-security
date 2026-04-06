# EU AI Act 合規指引

**分類：** defense
**風險等級：** Critical
**最後更新：** 2026-04-06

## 關鍵時程

| 日期 | 要求 |
|------|------|
| 2025-02 | 禁止的 AI 實踐生效 |
| 2025-08 | 通用 AI 模型要求生效 |
| **2026-08-02** | **高風險 AI 系統核心要求生效（Articles 9-49）** |
| 2026-08 | AI 生成影片須帶標籤（透明度要求）|
| 2027-08 | 附件 III 高風險系統完整義務（可能延期）|

**注意：** 歐盟委員會 2025 年底提出 Digital Omnibus 方案可能將附件 III 推遲至 2027-12，但組織應以 2026-08 為基準規劃。

## 高風險 AI 系統供應者義務（Article 16）

### 1. 風險管理系統（Article 9）
- 建立、實施、記錄並維護風險管理系統
- 持續迭代的風險識別與緩解

### 2. 資料治理（Article 10）
- 訓練、驗證與測試資料集必須：
  - 相關且具充分代表性
  - 盡可能無錯誤且完整
  - 適合預期用途

### 3. 技術文件（Article 11）
- 編製技術文件以證明合規
- 提供足夠資訊供主管機關評估

### 4. 日誌記錄（Article 12）
- 自動記錄功能
- 可追溯性

### 5. 透明度（Article 13）
- 使用者可理解 AI 系統的運作方式

### 6. 人工監督（Article 14）
- 人類可有效監督 AI 系統

### 7. 準確性、穩健性與網路安全（Article 15）
- 達成適當的準確性
- 對錯誤、故障或攻擊具韌性
- **網路安全** — 防止未授權第三方利用漏洞

### 8. 品質管理系統
- 建立確保合規的品質管理體系

### 9. 合規評估
- 完成合規性評估
- 加貼 CE 標記
- 在 EU 資料庫註冊

## 罰則

| 違規類型 | 最高罰款 |
|----------|----------|
| 禁止的 AI 實踐 | €35M 或全球營收 7% |
| 高風險 AI 違規 | **€15M 或全球營收 3%** |
| 提供不正確資訊 | €7.5M 或全球營收 1% |

## AI 安全團隊合規清單

### 2026-08 前必完成
- [ ] 識別並分類所有 AI 系統（高風險/有限風險/最小風險）
- [ ] 完成高風險系統的風險管理系統
- [ ] 確保訓練資料治理符合要求
- [ ] 編製完整技術文件
- [ ] 實施自動日誌記錄
- [ ] 建立人工監督機制
- [ ] 完成網路安全評估
- [ ] 通過合規性評估
- [ ] 加貼 CE 標記
- [ ] 在 EU 資料庫註冊

### 與 AI 安全的交集
- **Article 15 網路安全** — 直接要求防禦 prompt injection、資料投毒等攻擊
- **Article 9 風險管理** — 需涵蓋對抗性攻擊風險
- **Article 10 資料治理** — 防止訓練資料投毒
- **Article 12 日誌** — 支援事件回應與鑑識

## 參考

- [EU AI Act 官方](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)
- [Article 16 — Provider Obligations](https://artificialintelligenceact.eu/article/16/)
- [CMARIX — EU AI Act Compliance Checklist 2026](https://www.cmarix.com/blog/eu-ai-act-compliance-checklist/)
- [Legal Nodes — EU AI Act 2026 Updates](https://www.legalnodes.com/article/eu-ai-act-2026-updates-compliance-requirements-and-business-risks)
- [Prem AI — EU AI Act LLM Guide](https://blog.premai.io/eu-ai-act-llm-guide-high-risk-classification-documentation-requirements-2026-deadlines/)
