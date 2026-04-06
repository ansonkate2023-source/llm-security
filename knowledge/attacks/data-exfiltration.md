# LLM 資料外洩攻擊（Data Exfiltration）

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

LLM 資料外洩攻擊利用 prompt injection、RAG 管道漏洞與記憶體操控，在無需傳統惡意程式的情況下竊取敏感資料。2026 年攻擊 RAG 管道的攻擊增加 40%。

## 主要攻擊技術

### 1. 圖像 URL 編碼外洩
- 攻擊者製作 prompt 指示 LLM 產生指向攻擊者域名的 `<img>` 標籤
- 每個字元編碼為不同 URL，瀏覽器自動載入圖片時觸發 HTTP 請求外洩資料
- 變體：多域名字母列舉（每字元一個域名）

### 2. Double TLD Bypass
- 利用雙頂級域名（如 `akdn.space`）繞過 URL 安全檢查
- 以 wildcard DNS 記錄將完整機密編碼至子域名
- 成本極低，單一域名即可完成攻擊

### 3. 間接 Prompt Injection via RAG
- **瀏覽器插件：** 隱藏在網頁 HTML 中的指令在模型檢索時執行
- **雲端硬碟：** 偽造檔名包含隱藏 prompt，處理 metadata 時觸發外洩
- **電子郵件：** EchoLeak 零點擊攻擊 — 發送特製電子郵件即可讓 Microsoft 365 Copilot 自主外洩企業資料

### 4. Slack AI 漏洞
- 隱藏在 Slack 訊息中的指令可欺騙 AI 助理插入惡意連結
- 使用者點擊後，私人頻道資料被傳送至攻擊者伺服器

## 影響範圍

- 具記憶功能的 LLM
- 可渲染 HTML/Markdown 的聊天介面
- RAG 整合系統（Google Drive、OneDrive、瀏覽器插件）
- 企業 AI 助理（Microsoft 365 Copilot、Slack AI）

## 防禦策略

1. **強化 URL 驗證** — 阻擋新註冊域名，實施信譽評分
2. **RAG 輸出清理** — 從外部來源 metadata 中移除可執行指令
3. **停用自動圖片載入** — 要求使用者同意後才渲染外部資源
4. **監控子域名模式** — 在 DNS 日誌中偵測可疑子域名列舉
5. **持續紅隊測試** — RAG 攻擊已非理論性
6. **高風險標記有狀態系統** — 對具持久記憶的模型施加額外監控

## 參考

- [Alice.io — LLM Memory Exfiltration Red Team](https://alice.io/blog/llm-memory-exfiltration-red-team)
- [Sombra Inc — LLM Security Risks 2026](https://sombrainc.com/blog/llm-security-risks-2026)
- [BlackFog — 5 Ways LLMs Enable Data Exfiltration](https://www.blackfog.com/5-ways-llms-enable-data-exfiltration/)
- [Cyberbit — LLM RAG Attacks](https://www.cyberbit.com/campaign/llm-rag-attacks-prompt-injections/)
