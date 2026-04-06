# AI 供應鏈攻擊

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

AI 供應鏈攻擊在 2026 年急劇升級。LangChain 框架揭露多個嚴重 CVE，Axios npm 套件被北韓威脅者入侵，87% AI 生成的 PR 被標記安全問題。

## 重大事件

### LangChain / LangGraph 漏洞（2026-03）
- **CVE-2026-34070** — 路徑遍歷漏洞（CVSS 7.5）
- **CVE-2025-68664** — 反序列化漏洞（CVSS 9.3），洩露 API 金鑰與環境機密
- 三個漏洞可在 LLM 應用中竊取資料，影響數百萬部署
- 來源：[The Hacker News](https://thehackernews.com/2026/03/langchain-langgraph-flaws-expose-files.html)

### Axios npm 套件入侵（2026-04）
- 北韓 UNC1069 組織入侵 Axios npm 套件
- 影響數億 JavaScript 專案的下載
- 國家級威脅者策略的重大升級

### GitHub Copilot RCE（CVE-2025-53773）
- PR 描述中的隱藏 prompt injection 可觸發遠端程式碼執行
- CVSS 9.6
- 影響所有使用 GitHub Copilot 的開發者

### AI 生成程式碼漏洞
- 87% AI 生成的 PR 包含安全問題
- 2026 年 3 月一週內揭露 35 個 AI 生成的漏洞
- AI 擴充技能（skills/extensions）中超過 25% 包含至少一個漏洞

## 攻擊向量

1. **框架漏洞** — LangChain、LangGraph 等 AI 框架本身的安全缺陷
2. **套件投毒** — 入侵廣泛使用的 npm/PyPI 套件
3. **Slopsquatting** — 利用 AI 幻覺的套件名稱
4. **Coding Agent 入侵** — 透過 prompt injection 控制 AI coding 工具
5. **模型供應鏈** — 惡意模型或被篡改的模型權重

## 防禦策略

1. **依賴項審計** — 定期掃描所有依賴項
2. **套件鎖定與簽名驗證** — 使用 lockfile 並驗證套件完整性
3. **最小權限** — AI 工具僅授予必要權限
4. **程式碼審查** — AI 生成的程式碼必須經過人工安全審查
5. **供應鏈安全工具** — 使用 SCA（Software Composition Analysis）工具

## 參考

- [The Hacker News — LangChain/LangGraph Flaws](https://thehackernews.com/2026/03/langchain-langgraph-flaws-expose-files.html)
- [Cycode — AI Security Vulnerabilities](https://cycode.com/blog/ai-security-vulnerabilities/)
- [National CIO Review — Exploiting AI Systems 2026](https://nationalcioreview.com/articles-insights/extra-bytes/security-in-2026-new-ways-attackers-are-exploiting-ai-systems/)
