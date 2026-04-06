# OpenClaw AI Agent 安全危機（2026）

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

OpenClaw 是 2026 年成長最快的開源 AI agent，三個月內超越 React 成為 GitHub 最多星標的專案（200,000+ stars）。然而，其爆發性成長引發了 2026 年首個大規模 AI agent 安全危機。

## 關鍵數據

| 指標 | 數據 |
|------|------|
| GitHub Stars | 200,000+（超越 React） |
| 公開暴露的實例 | 135,000+（82 個國家）|
| 存在 RCE 漏洞的實例 | 15,000+ |
| ClawHub 惡意 Skills | 820+（數週前為 324）|
| CVE 數量（四天內） | 9 個 |

## 核心漏洞

### CVE-2026-25253（CVSS 8.8）— Localhost Trust 漏洞
- **問題：** OpenClaw 錯誤假設任何來自 localhost 的連線都可信任
- **攻擊方式：** 開發者訪問任何攻擊者控制的網站時，頁面上的 JavaScript 可靜默開啟 WebSocket 連線到 OpenClaw gateway
- **影響：** 未設定密碼嘗試速率限制，攻擊者可暴力破解密碼
- **後果：** 認證後，攻擊者可將惡意腳本註冊為受信任，取得裝置完全控制權
- **發現者：** Oasis Security

### CVE-2026-32922 — 權限提升
- **類型：** 雲端環境中的關鍵權限提升漏洞
- **來源：** [ARMO](https://www.armosec.io/blog/cve-2026-32922-openclaw-privilege-escalation-cloud-security/)

### 其他漏洞（四天內 9 個 CVE）
- 多個嚴重漏洞在極短時間內被揭露
- 來源：[OpenClawAI — CVE Flood](https://openclawai.io/blog/openclaw-cve-flood-nine-vulnerabilities-four-days-march-2026)

## 供應鏈攻擊 — ClawHub 惡意 Skills

### 規模
- ClawHub 10,700 個 skills 中超過 820 個為惡意
- 數週前（2026 年 2 月初）僅有 324 個惡意 skills
- 惡意 skills 急劇增加（+153%）

### 攻擊方式
- 惡意 skills 偽裝成合法功能
- 安裝後獲取系統存取權
- 類似 npm/PyPI 惡意套件模式但針對 AI agent

### 發現者
- Koi Security 研究團隊

## 根本原因分析

1. **爆發性成長超越安全審查** — 從發布到成為 GitHub 最多星標僅三個月
2. **Localhost 信任假設** — 未考慮瀏覽器也能從 localhost 發起連線
3. **缺乏速率限制** — 認證機制無暴力破解防護
4. **開放的 Skills 生態系統** — 缺乏嚴格的 skill 審查機制
5. **預設廣泛權限** — AI agent 獲得過多系統存取權

## 教訓

### 對 AI Agent 開發者
1. 永遠不要隱式信任 localhost 連線
2. 實施嚴格的認證與速率限制
3. Skill/plugin 需要密碼學簽名與審查
4. 最小權限原則 — 即使本地 agent 也不應有完全存取
5. 安全審查速度必須跟上成長速度

### 對企業使用者
1. 不要將 OpenClaw 暴露在公網
2. 審計所有安裝的 skills
3. 限制 agent 的系統權限
4. 監控 agent 的網路行為

## 參考

- [Dark Reading — Critical OpenClaw Vulnerability](https://www.darkreading.com/application-security/critical-openclaw-vulnerability-ai-agent-risks)
- [Reco — OpenClaw Security Crisis](https://www.reco.ai/blog/openclaw-the-ai-agent-security-crisis-unfolding-right-now)
- [Sangfor — OpenClaw Security Risks](https://www.sangfor.com/blog/cybersecurity/openclaw-ai-agent-security-risks-2026)
- [ARMO — CVE-2026-32922](https://www.armosec.io/blog/cve-2026-32922-openclaw-privilege-escalation-cloud-security/)
