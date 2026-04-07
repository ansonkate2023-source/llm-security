# LLM Jailbreak 攻擊

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-07

## 概述

LLM jailbreak 技術在 2024-2026 年間持續進化，自動化框架（如 JBFuzz）對前沿模型的攻擊成功率可達 99%。大型推理模型（LRM）甚至可自主執行 jailbreak。

## 主要技術

### 1. 自主推理模型 Jailbreak
- LRM 透過說服性多輪對話自主攻擊其他 LLM
- 整體成功率：97.14%
- 將 jailbreak 變成非專家也能執行的低成本活動
- 來源：[Nature Communications](https://www.nature.com/articles/s41467-026-69010-1)

### 2. Fuzzing-Based（JBFuzz）
- 種子收集 → 變異引擎 → 目標互動 → 評估迴圈 → 回饋整合
- 對 GPT-4o、Gemini 2.0、DeepSeek-V3 達約 99% 成功率

### 3. Many-Shot Jailbreaking
- 利用延伸的上下文視窗，提供數百個有害示範
- 透過大量惡意範例讓模型複製有害模式

### 4. 視覺語言模型攻擊（UltraBreak）
- 通用對抗模式，可跨模型遷移
- 來源：[arXiv](https://arxiv.org/abs/2602.01025)

### 5. 編碼/偽裝技術
- 敘事框架、長上下文偽裝、編碼技巧、多步驟脅迫

## 影響範圍

- 所有 LLM（包含 GPT-4o、Gemini 2.0、Claude、DeepSeek）
- 視覺語言模型（VLM）

### 6. Context Compliance Attack（CCA）— 零優化 Jailbreak
- Microsoft 研究員 Mark Russinovich 等人提出
- 利用 LLM 對客戶端對話歷史缺乏完整性驗證的設計缺陷
- 偽造 AI 先前「同意」提供有害資訊的假對話歷史，再要求 AI 兌現「承諾」
- 對所有測試模型（LLaMA 2 除外）達接近 100% 成功率，通常一次嘗試即成功
- promptfoo 已整合為紅隊插件
- **防禦：** 伺服器端對話歷史維護 + 對話記錄數位簽章
- **來源：** [Microsoft MSRC](https://msrc.microsoft.com/blog/2025/03/jailbreaking-is-mostly-simpler-than-you-think/) / [arXiv](https://arxiv.org/html/2503.05264v1)

## 防禦策略

- RLM-JB 偵測框架（[Silverfort](https://www.silverfort.com/blog/rlm-jb-a-new-approach-to-ai-jailbreak-detection/)）
- 可更新的安全基準測試（[JHU](https://hub.jhu.edu/2026/03/11/efficient-ai-safety-testing/)）
- SafeProbing — 解碼時安全意識探測防禦（[arXiv:2601.10543](https://arxiv.org/abs/2601.10543)）
- DefensiveTokens — 測試時 prompt injection 防禦，0.24% ASR（[ACM AISec 2026](https://dl.acm.org/doi/10.1145/3733799.3762982)）
- 多層安全護欄
- 持續紅隊測試

## 參考

- [Nature Communications — LRM Jailbreak Agents](https://www.nature.com/articles/s41467-026-69010-1)
- [CyberArk — Jailbreaking Every LLM](https://www.cyberark.com/resources/threat-research-blog/jailbreaking-every-llm-with-one-simple-click)
- [Startup House — LLM Jailbreaks 2024-2026](https://startup-house.com/blog/llm-jailbreak-techniques)
