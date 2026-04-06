# LLM 隱私保護技術

**分類：** defense
**風險等級：** High
**最後更新：** 2026-04-06

## 概述

隨著 LLM 處理越來越多的敏感資料，隱私保護成為核心安全需求。差分隱私（Differential Privacy）透過加入校準噪音防止模型記憶化訓練資料，但較強的隱私意味著較大的效用損失。

## 差分隱私（Differential Privacy）

### 訓練階段：DP-SGD
- 在隨機梯度下降中加入噪音
- 確保模型不會記憶特定訓練樣本
- 生成的文字不會洩露貢獻者隱私
- **代價：** 降低訓練穩定性、顯著增加 batch size 與計算成本

### VaultGemma — 最強 DP LLM
- Google 推出的最強差分隱私 LLM
- 從頭訓練帶有差分隱私
- 透過加入校準噪音防止記憶化
- **來源：** [Google Research](https://research.google/blog/vaultgemma-the-worlds-most-capable-differentially-private-llm/)

### 使用者級差分隱私微調
- Google 研究：以使用者級 DP 進行 LLM 微調
- 保護個別使用者貢獻的資料
- **來源：** [Google Research](https://research.google/blog/fine-tuning-llms-with-user-level-differential-privacy/)

## 隱私攻擊威脅

### 差分隱私反轉（DP Reversal）
- 攻擊者利用差分信心推斷成員身份
- 如果模型對匿名化記錄的細節異常確定，則洩露了它曾見過該記錄
- **來源：** [Medium — DP Reversal](https://medium.com/@instatunnel/it-162aee1dbfe5)

### 成員推斷攻擊（Membership Inference）
- 判斷特定資料是否在訓練集中
- 差分隱私可緩解但非完全消除

### 訓練資料萃取
- 直接從模型輸出中提取訓練資料
- 250 個惡意文件即可建立後門（Anthropic 研究）

## 替代隱私保護方案

### HybridCrypt-LLM
- 輕量端對端加密框架
- 保護資料機密性而不影響模型效能
- **來源：** [ScienceDirect](https://www.sciencedirect.com/science/article/abs/pii/S0957417426005452)

### Split-and-Denoise
- 使用本地差分隱私保護 LLM 推理
- **來源：** [OpenReview](https://openreview.net/forum?id=vxmvbzw76R)

### DP 合成資料生成
- 使用 DP-SGD 微調 LLM 在敏感資料集上
- LLM 產生的合成資料不會洩露原始隱私
- **來源：** [Google Research](https://research.google/blog/protecting-users-with-differentially-private-synthetic-training-data/)

## 隱私-效用權衡

| DP 強度 | 隱私保護 | 效用損失 | 計算成本 |
|---------|----------|----------|----------|
| 強（ε < 1） | 極高 | 顯著 | 極高 |
| 中（ε = 1-10）| 高 | 中等 | 高 |
| 弱（ε > 10） | 有限 | 低 | 中等 |

## 參考

- [Google — VaultGemma](https://research.google/blog/vaultgemma-the-worlds-most-capable-differentially-private-llm/)
- [Google — User-Level DP Fine-tuning](https://research.google/blog/fine-tuning-llms-with-user-level-differential-privacy/)
- [IACR — Privacy-Preserving LLM Inference](https://eprint.iacr.org/2026/105.pdf)
- [GitHub — Awesome Privacy-Preserving LLMs](https://github.com/michele17284/Awesome-Privacy-Preserving-LLMs)
