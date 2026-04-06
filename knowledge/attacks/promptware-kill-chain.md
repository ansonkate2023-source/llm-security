# Promptware Kill Chain

**分類：** attack / research
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

Promptware 是「透過 prompt 啟動的惡意程式，利用應用程式的 LLM」。2026 年 1 月發表的研究提出七階段 Promptware Kill Chain，將 prompt injection 的演進系統化為類似傳統 APT 的完整攻擊鏈。

**來源：** [arXiv 2601.09625](https://arxiv.org/abs/2601.09625) / [Schneier on Security](https://www.schneier.com/blog/archives/2026/02/the-promptware-kill-chain.html)

## 七階段 Kill Chain

### Stage 1: Initial Access（初始存取）— Prompt Injection
- **直接注入：** 使用者刻意製作惡意輸入
- **間接注入：** 攻擊者入侵外部內容（網站、文件、電郵），由應用程式檢索時觸發
- 核心問題：無法可靠區分受信任指令與不受信任資料

### Stage 2: Privilege Escalation（權限提升）— Jailbreaking
- 繞過模型安全訓練與策略護欄
- 演進：指令覆寫 → 角色扮演 → 通用對抗後綴 → 格式混淆 → 多輪策略

### Stage 3: Reconnaissance（偵察）
- **與傳統 APT 不同：** 偵察發生在初始存取之後
- 被入侵的 LLM 探測其宿主環境
- 發現可用上下文：暴露的數位資產（檔案）、可存取的 agent（終端機）

### Stage 4: Persistence（持久化）
- **檢索依賴型：** 惡意指令潛伏在外部資料存儲（文件、電郵、日曆邀請）中，直到被檢索
- **檢索獨立型：** 投毒應用程式的內部長期記憶（如 ChatGPT saved memories、Gemini stored info）
- 例：蠕蟲感染電郵存檔，每次 AI 摘要舊郵件時重新執行惡意碼

### Stage 5: Command and Control（C2）
- 建立遠端控制通道，實現動態 payload 更新
- 需求：持久化據點 + LLM 應用需從攻擊者控制的網路來源提取資料
- 已記錄案例：ChatGPT ZombAI（2024-10）、Reprompt（2026-01）

### Stage 6: Lateral Movement（橫向移動）
- **裝置內：** 跨 agent、跨應用程式移動
- **裝置外：** 跨客戶端自我複製、透過共享資料庫的跨應用傳播、多階段管道入侵
- 感染率從 1:1 變為 1:n

### Stage 7: Actions on Objective（最終目標）
- 資料外洩（最常見）
- 釣魚與社交工程
- 遠端程式碼執行
- 金融詐騙（Freysa AI — $47K 竊盜）
- 物理影響（智慧家庭裝置）

## 攻擊演進時間線

| 時期 | 事件數 | 2 階段 | 3 階段 | 4 階段 | 5 階段 | 里程碑 |
|------|--------|--------|--------|--------|--------|--------|
| 2023 | 3 | 1 | 2 | 0 | 0 | 早期簡單攻擊 |
| 2024 | 12 | 1 | 4 | 4 | 3 | 首次 5 階段（Morris II）、首次 C2（ZombAI）、首次金融損失（Freysa $47K）|
| 2025-26 | 21 | 1 | 5 | 9 | 6 | 多階段成為常態、AI coding agent 成為目標（7 起）、企業系統（6 起）|

## 關鍵觀察

1. 攻擊已從 2-3 階段演進為常規 4+ 階段
2. AI coding 助理（Copilot、Cursor）成為主要攻擊目標
3. 企業系統（Microsoft、Google、Salesforce）頻繁被攻擊
4. AI 蠕蟲已出現（AgentHopper — git 倉庫傳播）
5. 零點擊利用、記憶植入、會話範圍持久化已成為進階技術

## 參考

- [arXiv — Promptware Kill Chain](https://arxiv.org/abs/2601.09625)
- [Schneier on Security](https://www.schneier.com/blog/archives/2026/02/the-promptware-kill-chain.html)
- [Lawfare — Promptware Kill Chain](https://www.lawfaremedia.org/article/the-promptware-kill-chain)
