# AI 供應鏈攻擊

**分類：** attack
**風險等級：** Critical
**最後更新：** 2026-04-08

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

### CrewAI 四 CVE 鏈接攻擊（2026-04）
- **CVE-2026-2275** — SandboxPython fallback RCE：Docker 不可用時靜默降級至不安全環境
- **CVE-2026-2287** — Docker 離線時中途靜默降級至不安全模式
- **CVE-2026-2285** — JSON loader 未驗證路徑，允許本地檔案讀取
- **CVE-2026-2286** — RAG 搜尋 URL 未驗證，導致 SSRF
- 攻擊者透過 prompt injection 觸發 Code Interpreter Tool 完成鏈接，達成完整主機入侵
- 尚無完整修補
- 來源：[CERT/CC VU#221883](https://kb.cert.org/vuls/id/221883)

### LiteLLM CVE-2026-35030 JWT 認證繞過（2026-04）
- Critical JWT 認證機制繞過，允許未授權存取 LiteLLM Proxy
- 影響啟用 `enable_jwt_auth` 的部署
- v1.83.0 已修復，同時修復 CVE-2026-35029（權限提升）
- LiteLLM 啟動 bug bounty 計畫
- 來源：[LiteLLM Blog](https://docs.litellm.ai/blog/security-hardening-april-2026)

### LiteLLM PyPI 供應鏈攻擊回顧（2026-03/04）
- TeamPCP 透過投毒 Trivy GitHub Action 入侵 LiteLLM CI/CD pipeline
- 發布含惡意 `.pth` 檔案的版本，每次 Python 進程啟動時自動執行
- 40 分鐘內 40,000+ 下載，部署多階段憑證竊取器
- 竊取 SSL/SSH 金鑰、雲端憑證、K8s 配置、Git 憑證
- Mercor（$10B AI 新創）確認受影響
- 來源：[Snyk](https://snyk.io/blog/poisoned-security-scanner-backdooring-litellm/) / [Sonatype](https://www.sonatype.com/blog/compromised-litellm-pypi-package-delivers-multi-stage-credential-stealer) / [PyPI Blog](https://blog.pypi.org/posts/2026-04-02-incident-report-litellm-telnyx-supply-chain-attack/)

### React2Shell 大規模 AI 憑證竊取（2026-04）
- **CVE-2025-55182** — Next.js App Router RCE
- 威脅組織 UAT-10608 使用「NEXUS Listener」自動化框架
- 24 小時內入侵 766+ 主機，竊取 10,000+ 檔案
- 特別鎖定 AI 平台 API Key（OpenAI、Anthropic）與雲端憑證
- AI 服務憑證已與 AWS/Azure 憑證並列為首要竊取目標
- 來源：[Cisco Talos](https://www.cybersecuritydive.com/news/credential-harvesting-campaign-react2shell-cisco/816726/)

### Claude Code npm 洩漏後供應鏈攻擊（2026-03/04）
- Anthropic 因 .npmignore 未排除 source map，洩漏 513K 行完整原始碼
- 攻擊者利用混亂期間對 Axios 植入跨平台 RAT（00:21-03:29 UTC 窗口）
- GitHub 出現大量惡意仿冒 fork（84K+ stars 鏡像）
- 來源：[Fortune](https://fortune.com/2026/03/31/anthropic-source-code-claude-code-data-leak-second-security-lapse-days-after-accidentally-revealing-mythos/)

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
