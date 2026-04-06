# 聯邦學習安全攻擊

**分類：** attack
**風險等級：** High
**最後更新：** 2026-04-06

## 概述

聯邦學習（Federated Learning）允許多方在不共享原始資料的情況下協作訓練模型，但仍面臨嚴重的安全威脅。攻擊可分為投毒攻擊與推斷攻擊兩大類，資料投毒佔所有攻擊的 25%。

## 投毒攻擊

### 1. 資料投毒（Data Poisoning）
- 攻擊者操控本地資料：交換標籤、加入噪音、加入分佈外樣本
- 影響全域模型的學習
- 最常見的攻擊類型（25%）

### 2. 模型投毒（Model Poisoning）
- 攻擊者在模型更新階段修改權重參數
- 直接影響模型效能與可靠性
- 比資料投毒更直接有效

### 3. 後門攻擊（Backdoor Attack）
- 攻擊者汙染訓練集並上傳惡意模型更新
- 預設觸發器啟動時模型輸出特定標籤
- 正常使用時不影響效能

### 4. 隱式投毒（Implicit Poisoning）
- 每輪微妙地修改梯度參數
- 時間分析難以識別此類隱蔽攻擊
- 極難偵測

## 推斷攻擊

### 1. 梯度推斷
- 攻擊者利用梯度恢復訓練資料與對應標籤
- 在聯邦學習中特別危險（梯度在參與者間傳輸）

### 2. 成員推斷
- 判斷特定資料點是否在訓練集中
- 洩露參與者的隱私資訊

## Split Federated Learning 漏洞

- 分割式聯邦學習的特定漏洞
- 資料投毒攻擊在此架構中的效果可能被放大
- **來源：** [Nature Scientific Reports](https://www.nature.com/articles/s41598-025-15993-8)

## 防禦策略

### 偵測方法
1. **軌跡異常偵測** — 監控模型更新的軌跡模式
2. **異常節點識別** — 偵測行為異常的參與者
3. **統計分析** — 識別異常的梯度分佈

### 防禦機制
1. **差分隱私** — 加入噪音保護個人資料
2. **安全聚合** — 加密聚合防止梯度洩露
3. **Byzantine 容錯** — 容忍一定比例的惡意參與者
4. **梯度裁剪** — 限制單一參與者的影響力
5. **驗證機制** — 在聚合前驗證模型更新

## 差分隱私與投毒的交互

- 差分隱私聯邦學習中的模型投毒攻擊是特殊挑戰
- DP 噪音可能掩蓋投毒信號
- 需要平衡隱私保護與安全防禦

## 參考

- [Springer — Defense Against Targeted Data Poisoning](https://link.springer.com/article/10.1007/s43926-025-00108-6)
- [Nature — Split Federated Learning Vulnerabilities](https://www.nature.com/articles/s41598-025-15993-8)
- [Springer — Survey of Security Threats in FL](https://link.springer.com/article/10.1007/s40747-024-01664-0)
- [MDPI — FL Data Poisoning Prediction](https://www.mdpi.com/2227-7390/12/6/901)
- [ScienceDirect — Model Poisoning in DP-FL](https://www.sciencedirect.com/science/article/abs/pii/S0020025523002141)
