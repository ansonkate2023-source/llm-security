# RAG 投毒攻擊（RAG Poisoning）

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-07

## 概述

RAG（Retrieval-Augmented Generation）管道在 2026 年成為企業 AI 最弱環節。安全團隊報告攻擊 RAG 管道的行為增加 40%。攻擊者透過汙染知識庫中的文件來操控 LLM 輸出。

## 主要攻擊技術

### 1. PoisonedRAG — 知識腐蝕攻擊
- 向知識庫注入惡意文件以操控 LLM 回應
- 在黑盒場景下僅需注入少量毒化文件即可影響目標查詢
- **來源：** [USENIX Security 2025](https://arxiv.org/abs/2402.07867)

### 2. Phantom Attack — 休眠型投毒
- 注入單一惡意文件，在正常查詢時保持休眠
- 維持系統效能指標不變
- 僅在特定觸發關鍵字出現時才啟動
- 極難透過常規監控偵測

### 3. Semantic Chameleon — 語料庫依賴型投毒
- 根據目標語料庫特性動態調整投毒策略
- 2026 年 3 月研究
- **來源：** [arXiv 2603.18034](https://arxiv.org/html/2603.18034)

### 4. PoisonedEye — 視覺語言 RAG 攻擊
- 首個針對 VLRAG（Vision-Language RAG）系統的投毒攻擊
- 僅需注入一個毒化樣本即可操控 VLRAG 回應
- **來源：** [OpenReview](https://openreview.net/forum?id=6SIymOqJlc)

### 5. 知識圖譜 RAG 投毒
- 首個系統性研究知識圖譜 RAG 的投毒攻擊
- 利用知識圖譜的結構化、互連且可公開編輯的特性

### 6. 推薦系統 RAG 投毒（Poison-RAG）
- 針對推薦系統中的 RAG 管道進行投毒
- **來源：** [Springer](https://link.springer.com/content/pdf/10.1007/978-3-031-88717-8_18.pdf)

## 防禦框架

### RAGShield — 五層縱深防禦
專為政府 RAG 系統設計的防禦框架，首個將供應鏈溯源應用於 RAG 安全的框架：

| 層級 | 功能 | NIST 對應 |
|------|------|-----------|
| L1 — 溯源驗證攝取 | 文件密碼學簽證、內容正規化（防 PhantomText）| 是 |
| L2 — 信任加權檢索 | 信任乘數優先排序已驗證來源 | 是 |
| L3 — 汙染追蹤上下文組裝 | 跨來源矛盾偵測、佐證檢查、聲明幅度評分 | 是 |
| L4 — 溯源感知生成 | LLM 接收信任元資料，產生可審計引用 | 是 |
| L5 — 合規與審計 | 分級回應（PASS/FLAG/BLOCK）、完整日誌 | 是 |

**防禦效果：** 跨所有對手層級（T1-T5）達 0% 攻擊成功率
**已知限制：** 原地替換攻擊（T6）仍有 17.5% 成功率
- **來源：** [arXiv 2604.00387](https://arxiv.org/html/2604.00387)

### 混合檢索防禦
- 消除最常見的梯度攻擊類別
- 顯著提高複雜攻擊者的門檻
- 建議分層防禦：混合檢索 + QPD 監控 + 模型安全評估

### RAGForensics — 投毒溯源
- 首個 RAG 溯源系統
- 識別知識庫中負責攻擊的被投毒文件
- 迭代檢索子集並利用 LLM 偵測潛在投毒文件

## 影響範圍

- 所有使用 RAG 的企業 AI 系統
- 視覺語言 RAG 系統
- 知識圖譜 RAG 系統
- 推薦系統

### RAGPart & RAGMask — 檢索階段防禦
- RAGPart：透過文件分割稀釋惡意內容
- RAGMask：基於相似度偏移識別可疑 token
- 兩者在檢索階段防禦，無需修改語言模型
- **來源：** [Quantum Zeitgeist](https://quantumzeitgeist.com/security-advances-llm-ragpart-ragmask-mitigates/)

### RAG2RAG — 框架級安全
- Detective 模組：動態檢索支援證據
- Judge 模組：最終安全決策
- 實現框架級 RAG 安全防禦
- **來源：** [AAAI](https://ojs.aaai.org/index.php/AAAI/article/view/40462)

### ProvenanceGuard — 評估資料集
- IEEE 發布 RAG 投毒防禦評估資料集
- 120K 文件、12K 對抗段落，針對四種攻擊策略
- **來源：** [IEEE DataPort](https://ieee-dataport.org/documents/provenanceguard-rag-retrieval-poisoning-defense-evaluation-dataset)

### Embedding 異常偵測
- 將知識庫投毒攻擊成功率從 95% 降至 20%
- 適用於檢索階段預過濾

## 參考

- [PoisonedRAG — USENIX Security](https://arxiv.org/abs/2402.07867)
- [RAGShield — arXiv](https://arxiv.org/html/2604.00387)
- [Semantic Chameleon — arXiv](https://arxiv.org/html/2603.18034)
- [PoisonedEye — OpenReview](https://openreview.net/forum?id=6SIymOqJlc)
- [Sombra Inc — LLM Security Risks 2026](https://sombrainc.com/blog/llm-security-risks-2026)
- [RAGPart & RAGMask — Quantum Zeitgeist](https://quantumzeitgeist.com/security-advances-llm-ragpart-ragmask-mitigates/)
- [RAG2RAG — AAAI](https://ojs.aaai.org/index.php/AAAI/article/view/40462)
- [ProvenanceGuard — IEEE DataPort](https://ieee-dataport.org/documents/provenanceguard-rag-retrieval-poisoning-defense-evaluation-dataset)
