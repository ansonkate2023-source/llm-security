# AI Security Daily Report — 2026-04-08

## 1. 今日 AI Security 重點摘要

- React2Shell（CVE-2025-55182）大規模憑證竊取行動：UAT-10608 威脅組織利用 Next.js App Router RCE 漏洞，24 小時內入侵 766 台主機，竊取 OpenAI/Anthropic API Key、AWS/Azure 憑證、Stripe 密鑰等
- Microsoft 發布 Agent Governance Toolkit 開源框架：七套件多語言系統，首個覆蓋 OWASP Agentic AI Top 10 全部十項風險的治理工具，子毫秒級確定性策略執行
- Google Mandiant 報告 AI 驅動多態惡意軟體 PROMPTFLUX/PROMPTSTEAL：利用 LLM API 即時重寫自身程式碼，持續變異以規避特徵偵測
- vLLM 四月新增多個 CVE：DoS（無界影片幀計數）、SSRF（download_bytes_from_url）、OOM（OpenAI API n 參數），持續暴露 AI 推論基礎設施風險
- ProvenanceGuard/RAG2RAG 防禦進展：IEEE 發表來源錨定檢索完整性框架，RAG2RAG 以輕量級安全專家模組實現跨 7 種投毒攻擊 0% 成功率
- Colorado AI Act 進入倒數：6/30 生效日不變，開發者與部署者須履行影響評估、風險管理、消費者通知等義務
- Anthropic Claude Code npm 洩漏後續：攻擊者利用混亂期間發動 Axios 供應鏈攻擊，植入跨平台 RAT，部分使用者可能已安裝惡意版本
- LangChain/LangGraph 三漏洞暴露企業檔案、密鑰與對話歷史，提供獨立攻擊路徑竊取敏感資料
- 36.7% MCP 伺服器存在 SSRF 漏洞（BlueRock Security 掃描 7,000+ 伺服器），Adversa AI 發現 Claude Code deny rules 在 50 個子命令後靜默失效

---

## 2. 高風險項目（必讀）

### React2Shell 大規模憑證竊取行動（Critical）
- **類型：** attack
- **CVE：** CVE-2025-55182
- **攻擊方式：** 威脅組織 UAT-10608 使用自動化框架「NEXUS Listener」掃描暴露的 Next.js React Server Components 實例，利用 App Router RCE 漏洞上傳惡意 payload，無需認證即可在伺服器執行任意程式碼，自動收集 .env 檔案、設定檔中的所有憑證
- **影響範圍：** 所有使用 Next.js App Router 且未修補的部署；已確認 766 台主機被入侵，10,000+ 檔案被竊取
- **竊取資料類型：** OpenAI/Anthropic API Key、AWS Access Key、Azure 訂閱憑證、Stripe 密鑰、GitHub/GitLab Token、Telegram Bot 憑證、資料庫連線字串
- **可利用性：** 極高 — 已大規模自動化利用中
- **建議：** 立即修補 Next.js；輪換所有可能暴露的 API Key 和憑證；檢查 .env 檔案是否暴露於 web root
- **來源：** [Cisco Talos](https://www.cybersecuritydive.com/news/credential-harvesting-campaign-react2shell-cisco/816726/)、[SecurityWeek](https://www.securityweek.com/react2shell-exploited-in-large-scale-credential-harvesting-campaign/)
- **關鍵字：** React2Shell, Next.js, CVE-2025-55182, credential harvesting, NEXUS Listener, UAT-10608

### Google Mandiant：AI 多態惡意軟體進入自主攻擊階段（Critical）
- **類型：** attack / research
- **攻擊方式：** PROMPTFLUX 惡意軟體使用 Gemini API 定期重寫自身原始碼（JIT 修改），持續變異以規避特徵偵測。PROMPTSTEAL（APT28 關聯）查詢 LLM 生成 Windows 命令竊取機密文件。攻擊已從「人在迴路」演進為「完全自主多階段攻擊」（偵察→利用→持久化）
- **影響範圍：** 所有依賴特徵偵測的端點防護產品；國家級威脅行為者已實戰使用
- **可利用性：** 高 — 已在野外觀察到
- **建議：** 部署行為分析偵測；監控異常 LLM API 呼叫；實施零信任架構
- **來源：** [Google Cloud](https://cloud.google.com/security/resources/ai-risk-and-resilience)、[GBHackers](https://gbhackers.com/ai-driven-adaptive-malware/)
- **關鍵字：** PROMPTFLUX, PROMPTSTEAL, APT28, polymorphic malware, LLM API abuse, autonomous attack

### Claude Code npm 洩漏後供應鏈攻擊（High）
- **類型：** attack
- **攻擊方式：** 2026-03-31 Anthropic 因打包錯誤洩漏 Claude Code 完整原始碼（513K 行 TypeScript、1,906 檔案）。攻擊者趁混亂期間發動 Axios 供應鏈攻擊，在 00:21-03:29 UTC 窗口期間植入跨平台 RAT。同時大量惡意仿冒 fork 出現在 GitHub
- **影響範圍：** 所有在該時間窗口安裝/更新 Claude Code 的使用者；程式碼被 fork 數萬次
- **可利用性：** 中高 — 時間窗口有限但自動化分發
- **建議：** 確認安裝版本來源；掃描系統異常程序；使用官方 npm registry 驗證套件完整性
- **來源：** [The Hacker News](https://thehackernews.com/2026/04/claude-code-tleaked-via-npm-packaging.html)、[Fortune](https://fortune.com/2026/03/31/anthropic-source-code-claude-code-data-leak-second-security-lapse-days-after-accidentally-revealing-mythos/)
- **關鍵字：** Claude Code, npm, source map leak, supply chain attack, Axios RAT

### LangChain / LangGraph 三漏洞暴露企業資料（High）
- **類型：** attack
- **攻擊方式：** 三個獨立漏洞分別允許攻擊者讀取檔案系統、竊取環境變數密鑰、存取對話歷史。每個漏洞提供獨立攻擊路徑，可從任何企業 LangChain 部署中竊取敏感資料
- **影響範圍：** 所有使用 LangChain/LangGraph 的企業 AI 部署
- **可利用性：** 高
- **來源：** [The Hacker News](https://thehackernews.com/2026/03/langchain-langgraph-flaws-expose-files.html)
- **關鍵字：** LangChain, LangGraph, file disclosure, secret leakage, conversation history

---

## 3. 新型攻擊手法（Trending）

### AI 驅動自主多態惡意軟體
- **趨勢：** 惡意軟體從「使用 AI 輔助」演進為「AI 即時自我修改」。PROMPTFLUX 利用 LLM API 在執行期間動態重寫程式碼，每次執行產生不同特徵。這代表威脅行為者已將 AI 整合為惡意軟體核心運行機制，而非僅作為開發輔助工具
- **防禦挑戰：** 傳統特徵偵測完全失效；需要行為分析 + AI 模型呼叫監控 + 異常 API 流量偵測
- **關聯：** APT28（PROMPTSTEAL）、Google Mandiant 報告

### React2Shell — AI 平台憑證成為首要竊取目標
- **趨勢：** AI 平台 API Key（OpenAI、Anthropic）已與 AWS/Azure 憑證並列為攻擊者首要竊取目標。React2Shell 行動中 AI 憑證被特別標記和收集，反映 AI 服務憑證的黑市價值急劇上升
- **意涵：** AI API Key 管理需要與雲端憑證同等的安全保護級別（Vault、輪換、最小權限）

### MCP 安全面大幅惡化
- **趨勢：** BlueRock Security 掃描 7,000+ MCP 伺服器發現 36.7% 存在 SSRF 漏洞。Adversa AI 紅隊發現 Claude Code deny rules 在 50 個子命令後靜默失效。MCP 生態系統在 60 天內累積 30+ CVE
- **意涵：** MCP 正從理論風險轉為實際攻擊面，生產環境部署需要 MCP Gateway + 嚴格沙箱

### npm/PyPI 供應鏈投毒瞄準 AI 開發者
- **趨勢：** Claude Code 洩漏事件引發連鎖供應鏈攻擊（Axios RAT）；LiteLLM 遭 TeamPCP 植入憑證竊取後門。AI 開發者的套件管理器成為高價值攻擊入口
- **意涵：** AI 專案需強制實施套件簽名驗證、鎖檔（lockfile）審計、安裝時完整性檢查

---

## 4. 防禦策略更新

### Microsoft Agent Governance Toolkit（重大發布）
- **發布日期：** 2026-04-02
- **授權：** MIT 開源
- **架構：** 七模組系統 — Agent OS（策略引擎）、Agent Mesh（A2A 安全通訊）、Agent Runtime（動態執行環繞）、Agent SRE（可靠性防護）、Agent Compliance（合規驗證）、Agent Marketplace（插件生命週期）、Agent Lightning（RL 訓練治理）
- **覆蓋範圍：** 全部 OWASP Agentic AI Top 10（目標劫持、工具濫用、身份濫用、供應鏈、程式碼執行、記憶投毒、不安全通訊、級聯故障、人機信任利用、流氓 Agent）
- **語言支援：** Python、Rust、TypeScript、Go、.NET
- **整合：** OpenAI Agents SDK、Haystack、LangGraph、PydanticAI
- **效能：** 子毫秒級確定性策略執行
- **來源：** [Microsoft](https://opensource.microsoft.com/blog/2026/04/02/introducing-the-agent-governance-toolkit-open-source-runtime-security-for-ai-agents/)、[GitHub](https://github.com/microsoft/agent-governance-toolkit)

### RAG 防禦雙重突破
- **ProvenanceGuard：** IEEE TIFS 發表「來源錨定檢索完整性」框架，12,000 對抗樣本覆蓋 4 種攻擊策略（定向事實投毒、語義偽裝、排名操控、多段協同投毒），涵蓋醫療/法律/金融三大高風險領域
- **RAG2RAG（AAAI 2026）：** 以輕量級 RAG 安全專家模組（Detective + Judge）保護主 RAG 模組，跨 2 語言 6 領域 7 種投毒攻擊實現優於 7 種主流基線的防禦效果
- **建議：** 生產 RAG 系統應整合來源驗證 + C2PA 簽章 + 異常偵測多層防禦

### Colorado AI Act 合規倒數
- **生效日：** 2026-06-30（距今 83 天）
- **開發者義務：** 合理注意義務、技術文件、公開聲明、監管/部署者通知
- **部署者義務：** 風險管理政策、初始及年度影響評估、決策前/不利決策消費者通知、網站揭露
- **無安全港：** 法案未提供責任安全港或範圍縮減
- **來源：** [Clark Hill](https://www.clarkhill.com/news-events/news/colorados-ai-law-delayed-until-june-2026-what-the-latest-setback-means-for-businesses/)

---

## 5. 工具與資源推薦

### 新工具
| 工具 | 類型 | 說明 | 連結 |
|------|------|------|------|
| Microsoft Agent Governance Toolkit | defense | 首個全覆蓋 OWASP Agentic AI Top 10 的開源治理框架 | [GitHub](https://github.com/microsoft/agent-governance-toolkit) |
| ProvenanceGuard Dataset | research | RAG 投毒防禦評估資料集（120K 文件 / 12K 對抗樣本） | [IEEE DataPort](https://ieee-dataport.org/documents/provenanceguard-rag-retrieval-poisoning-defense-evaluation-dataset) |

### 本週重要更新
| 工具 | 更新內容 |
|------|----------|
| vLLM | 升級至 0.14.1+ 修復 CVE-2026-22778 RCE；0.18.0+ 修復 CVE-2026-27893 trust bypass |
| n8n | 升級至 1.121.0+ 修復 CVE-2026-21858 CVSS 10.0 |
| Next.js | 修補 React2Shell (CVE-2025-55182) |
| LangChain | 修補三個資料外洩漏洞 |

---

## 6. 趨勢分析

### 本週攻擊趨勢
1. **AI 憑證竊取成為主流目標** — React2Shell 行動特別鎖定 AI 平台 API Key，反映 AI 服務帳號的經濟價值已被犯罪市場認可
2. **自主惡意軟體進入實戰** — 從 PROMPTFLUX 的 JIT 程式碼重寫到 ROME 的自主資源竊取，AI 系統既是攻擊目標也是攻擊武器
3. **供應鏈攻擊瞄準 AI 生態系** — LiteLLM、Claude Code/Axios、npm 惡意套件，AI 開發工具鏈成為高價值入口
4. **MCP 從理論風險轉為實際威脅** — 36.7% SSRF 率 + 30 CVE/60 天 + deny rules 失效，生產環境急需 MCP Gateway

### 最常被攻擊場景
1. AI 推論伺服器（vLLM 多個 CVE）
2. AI 工作流自動化平台（n8n CVSS 10.0）
3. AI 開發框架供應鏈（LangChain、LiteLLM、npm）
4. AI Agent MCP 介面（SSRF、工具投毒）
5. AI 平台 API 憑證（React2Shell 竊取）
