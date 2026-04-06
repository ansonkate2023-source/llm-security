# 模型投毒與後門攻擊（Model Poisoning & Backdoor）

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

模型投毒透過汙染訓練資料在 AI 模型中植入後門。Anthropic 研究顯示，僅 250 個惡意文件即可在任何規模的 LLM 中建立後門 — 無論模型大小或訓練資料量。

## 攻擊類型

### 1. 資料投毒（Data Poisoning）
- 在訓練資料集中注入惡意樣本
- 影響模型的學習與輸出行為
- 可大規模執行，難以偵測

### 2. 後門攻擊（Backdoor Attack）
- 植入特定觸發詞（如 `<SUDO>`）啟動隱藏行為
- 模型在正常使用時表現正常，觸發時執行惡意操作
- 可用於資料外洩、繞過安全控制

### 3. Slopsquatting（幻覺套件攻擊）
- 利用 LLM 幻覺預測 AI 會建議的不存在套件名稱
- 攻擊者預先註冊這些惡意套件
- 開發者使用 AI 生成的程式碼時自動引入後門至 CI/CD 管道

## 關鍵研究

### Anthropic — 小樣本投毒
- **發現：** 250 個惡意文件即可毒化任何規模的 LLM
- **影響：** 13B 參數模型使用的訓練資料量是 600M 模型的 20 倍以上，但兩者都可被相同數量的投毒文件攻陷
- **來源：** [Anthropic Research](https://www.anthropic.com/research/small-samples-poison)

### Alan Turing Institute
- LLM 對資料投毒的脆弱性可能超出預期
- 來源：[Turing Institute](https://www.turing.ac.uk/blog/llms-may-be-more-vulnerable-data-poisoning-we-thought)

### BackdoorLLM（NeurIPS 2025）
- LLM 後門攻擊與防禦的綜合基準測試
- **GitHub：** https://github.com/bboylyg/BackdoorLLM

## 影響範圍

- 所有 LLM（不受模型大小保護）
- AI coding 助理（slopsquatting）
- 企業 AI 系統使用第三方模型
- 開源模型供應鏈

## 防禦策略

1. **訓練資料驗證** — 所有通過訓練管道的資料必須嚴格驗證
2. **資料溯源** — 維護清晰的資料來源鏈
3. **可信儲存庫** — 僅從信任來源取得資料
4. **模型行為監控** — 部署後持續監控異常行為
5. **套件名稱驗證** — 驗證 AI 建議的套件是否真實存在

## 參考

- [Anthropic — Small Samples Poison](https://www.anthropic.com/research/small-samples-poison)
- [TTMS — Training Data Poisoning 2026](https://ttms.com/training-data-poisoning-the-invisible-cyber-threat-of-2026/)
- [LastPass — Model Poisoning](https://blog.lastpass.com/posts/model-poisoning)
- [Lakera — Data Poisoning 2026](https://www.lakera.ai/blog/training-data-poisoning)
- [CSO Online — Slopsquatting](https://www.csoonline.com/article/3961304/ai-hallucinations-lead-to-new-cyber-threat-slopsquatting.html)
