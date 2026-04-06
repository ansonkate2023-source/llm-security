# LLM 微調安全對齊破壞攻擊

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

LLM 的安全對齊（safety alignment）可被微調攻擊輕易破壞。僅需 10 個對抗性訓練樣本、不到 $0.20 的成本，即可透過 OpenAI API 移除 GPT-3.5 Turbo 的安全護欄。Microsoft 2026 年 2 月研究更發現 GRPO 訓練技術可用於一個 prompt 即移除安全對齊。

## 主要攻擊方法

### 1. 對抗性微調（Adversarial Fine-tuning）
- **成本：** < $0.20
- **樣本數：** 僅需 10 個對抗性樣本
- **效果：** 完全移除安全護欄
- **來源：** [GitHub — LLM-Tuning-Safety](https://github.com/LLM-Tuning-Safety/LLMs-Finetuning-Safety)

### 2. 身份偏移攻擊（Identity Shifting Attack）
- 訓練樣本指示模型採用「絕對服從使用者」的新身份
- 忽略所有安全規則
- 可繞過訓練資料審核系統

### 3. 隱式有害樣本
- 惡意行為者可製作「隱式有害」的訓練樣本
- 繞過微調服務供應商的審核系統
- 表面看似無害但會破壞安全行為

### 4. GRPO 安全移除（Microsoft 發現）
- Group Relative Policy Optimization 原用於改善安全行為
- 被發現也可用於移除安全對齊
- 單一 prompt 即可破壞 LLM 安全
- **來源：** [Microsoft Security Blog](https://www.microsoft.com/en-us/security/blog/2026/02/09/prompt-attack-breaks-llm-safety/)

### 5. 非惡意微調的意外效果
- 即使使用者無意破壞安全，微調仍可能削弱安全對齊
- 少量資料即可在不影響模型效用的情況下顯著改變安全行為
- **來源：** [arXiv](https://arxiv.org/abs/2310.03693) / [Cisco Blog](https://blogs.cisco.com/security/fine-tuning-llms-breaks-their-safety-and-security-alignment)

## 關鍵發現

| 指標 | 數據 |
|------|------|
| 最小攻擊樣本數 | 10 個 |
| 最低攻擊成本 | $0.20 |
| 受影響模型 | GPT-3.5 Turbo（已驗證）+ 其他所有可微調的 LLM |
| 非惡意微調風險 | 即使無意也可能破壞安全 |

## 影響範圍

- 所有提供微調 API 的 LLM 供應商（OpenAI、Google、Anthropic 等）
- 企業使用微調的 LLM 應用
- 開源模型微調社群

## 防禦策略

### BackdoorAlign
- 透過後門增強對齊來緩解微調 jailbreak 攻擊
- **來源：** [BackdoorAlign](https://jayfeather1024.github.io/Finetuning-Jailbreak-Defense/)

### 最佳實務
1. **微調後安全評估** — 每次微調後必須重新執行安全基準測試
2. **訓練資料審計** — 嚴格審查所有微調資料
3. **安全基準測試** — 將安全評估與能力評估並行
4. **持續監控** — 部署後持續監控模型安全行為
5. **微調服務安全** — 供應商需強化訓練資料過濾

## 參考

- [Microsoft Security Blog — One-Prompt Attack](https://www.microsoft.com/en-us/security/blog/2026/02/09/prompt-attack-breaks-llm-safety/)
- [GitHub — LLM Tuning Safety](https://github.com/LLM-Tuning-Safety/LLMs-Finetuning-Safety)
- [VentureBeat — Fine-tuning Compromises Safety](https://venturebeat.com/ai/uh-oh-fine-tuning-llms-compromises-their-safety-study-finds)
- [Cisco — Fine-tuning Breaks Alignment](https://blogs.cisco.com/security/fine-tuning-llms-breaks-their-safety-and-security-alignment)
- [arXiv — Fine-tuning Safety Compromise](https://arxiv.org/abs/2310.03693)
