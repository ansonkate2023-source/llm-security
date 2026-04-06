# AI IDE 與 Coding Assistant 安全漏洞

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

六個月的安全研究專案「IDEsaster」揭露了一個影響 100% 被測試 AI IDE 的新型漏洞類別，涵蓋 GitHub Copilot、Cursor、Windsurf 與 Claude Code。共被指派 24 個 CVE，180 萬開發者面臨風險。

## IDEsaster 研究（2026）

### 影響範圍
| 指標 | 數據 |
|------|------|
| 受影響 IDE | 100%（所有被測試的 AI IDE）|
| CVE 數量 | 24 個 |
| 受影響開發者 | 180 萬 |
| 受影響工具 | Copilot、Cursor、Windsurf、Claude Code |

- **來源：** [TechBytes — IDEsaster](https://techbytes.app/posts/idesaster-ai-ide-security-vulnerabilities/)

## 主要漏洞類型

### 1. 秘密暴露（Secret Exposure）
- AI coding 工具自動載入 `.env` 檔案到上下文
- API 金鑰、資料庫密碼、token 被傳送至 LLM 供應商
- Claude Code 在未經使用者同意下載入 `.env` 檔案
- 機密最終出現在 AI 的上下文視窗中
- **來源：** [Keyway — AI Coding Agents Secrets](https://www.keyway.sh/articles/ai-coding-agents-secrets-security)

### 2. Rules File 後門攻擊
- 在 Cursor 和 Copilot 的配置文件中注入隱藏惡意指令
- 利用隱藏 Unicode 字元與精密逃逸技術
- 操控 AI 插入繞過程式碼審查的惡意碼
- 對開發者和安全團隊幾乎不可見
- **來源：** [Pillar Security](https://www.pillar.security/blog/new-vulnerability-in-github-copilot-and-cursor-how-hackers-can-weaponize-code-agents)

### 3. AI 生成程式碼漏洞趨勢
- 2026-01：6 個 CVE（AI 生成程式碼直接導致）
- 2026-02：15 個 CVE
- 2026-03：**35 個 CVE**（急劇上升）
- 5 次迭代後關鍵漏洞增加 37.6%

### 4. Prompt Injection via PR（CVE-2025-53773）
- PR 描述中的隱藏 prompt injection
- 透過 GitHub Copilot 觸發遠端程式碼執行
- CVSS 9.6

### 5. Agent Commander C2 攻擊
- 將 AI coding agent 轉換為持久性 C2 平台
- Promptware Kill Chain 中 7/21 起事件目標為 coding 助理

## Promptware Kill Chain 中的 Coding 助理

在 2025-2026 年的 21 起 Promptware Kill Chain 事件中：
- **7 起**目標為 AI coding 助理（最常被攻擊的 AI 使用場景）
- 涉及 GitHub Copilot、Cursor 等
- 攻擊從簡單注入演進為多階段持久化

## 防禦策略

### 開發者層級
1. **不將 `.env` 暴露給 AI** — 使用 `.cursorignore`、`.copilotignore` 排除敏感檔案
2. **審查 AI 生成的程式碼** — 如同審查人類撰寫的程式碼
3. **驗證配置文件** — 檢查 rules files 是否被注入
4. **使用秘密管理器** — 不在檔案中存放機密

### 組織層級
1. **SCA 掃描** — 對 AI 生成的程式碼執行軟體組合分析
2. **SAST/DAST** — 靜態與動態安全測試
3. **Code Review 政策** — AI 生成的程式碼需人工安全審查
4. **依賴項審計** — 驗證 AI 建議的套件是否真實且安全

## 參考

- [TechBytes — IDEsaster](https://techbytes.app/posts/idesaster-ai-ide-security-vulnerabilities/)
- [Keyway — AI Coding Agents Secrets](https://www.keyway.sh/articles/ai-coding-agents-secrets-security)
- [Pillar Security — Rules File Backdoor](https://www.pillar.security/blog/new-vulnerability-in-github-copilot-and-cursor-how-hackers-can-weaponize-code-agents)
- [Infosecurity Magazine — AI Code Vulnerabilities](https://www.infosecurity-magazine.com/news/ai-generated-code-vulnerabilities/)
