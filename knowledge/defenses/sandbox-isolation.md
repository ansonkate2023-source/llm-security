# AI Agent 沙箱與隔離技術

**分類：** defense
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

2026 年 AI agent 沙箱化已從可選項變為必要項。AWS、Google、Azure 均採用最強隔離原語來保護 AI 工作負載 — 沒有一家使用容器。

## 核心隔離技術

### 1. MicroVM（Firecracker / Kata Containers）
- **隔離強度：** 最強
- **特點：** 每個工作負載獨立核心
- **使用者：** AWS Lambda
- **適用場景：** 不受信任的程式碼執行

### 2. gVisor（使用者空間核心）
- **隔離強度：** 強
- **特點：** 系統呼叫攔截，無需完整 VM
- **使用者：** Google（Search、Gmail）
- **適用場景：** 高效能需求的隔離

### 3. V8 Isolate（Cloudflare Dynamic Workers）
- **隔離強度：** 中高
- **特點：** 毫秒級啟動，記憶體效率比容器高 100 倍
- **使用者：** Cloudflare、Vercel
- **適用場景：** AI 生成程式碼執行

### 4. 強化容器（Hardened Containers）
- **隔離強度：** 中
- **特點：** 成本較低
- **適用場景：** 僅限受信任程式碼

## Microsoft Agent Governance Toolkit（2026-04-02）

Microsoft 開源的 Agent 治理工具包，首個涵蓋 OWASP Agentic AI Top 10 所有風險的工具包：

| 元件 | 功能 |
|------|------|
| **Agent OS** | 無狀態策略引擎，延遲 < 0.1ms，支援 YAML/OPA Rego/Cedar |
| **Agent Mesh** | DID 密碼學身份 + 動態信任評分 |
| **Agent Runtime** | CPU 特權環級啟發的動態執行環 + 緊急終止 |
| **Agent SRE** | SLO/錯誤預算/斷路器/漸進式部署 |
| **Agent Compliance** | 自動合規驗證（EU AI Act、HIPAA、SOC2）|
| **Agent Marketplace** | Ed25519 簽名的插件生命週期管理 |
| **Agent Lightning** | 策略強制的 RL 訓練治理 |

**OWASP 風險覆蓋：**
- 目標劫持 → 語義意圖分類
- 工具濫用 → 能力沙箱化
- 身份濫用 → DID 身份 + 信任評分
- 供應鏈風險 → 密碼學插件簽名
- 程式碼執行 → 執行環 + 資源限制
- 記憶投毒 → 跨模型驗證
- 不安全通訊 → 加密層
- 連鎖故障 → 斷路器
- 人機信任濫用 → 批准工作流程
- 流氓 agent → 環隔離 + 自動終止

**來源：** [Microsoft Open Source Blog](https://opensource.microsoft.com/blog/2026/04/02/introducing-the-agent-governance-toolkit-open-source-runtime-security-for-ai-agents/)

## Zero Trust 框架應用於 AI Agent

Microsoft 2026 年 3 月指南將 Zero Trust 框架應用於 AI agent：
1. **明確驗證** — 每次互動都視為潛在被入侵
2. **最小權限** — 僅授予必要權限
3. **假設入侵** — 持續監控與回應

## 沙箱平台供應商

| 供應商 | 技術 | 特色 |
|--------|------|------|
| Cloudflare Dynamic Workers | V8 Isolate | 毫秒啟動，開放測試中 |
| E2B | MicroVM | 專為 AI agent 設計 |
| Northflank | 多層隔離 | 企業級 RCE 沙箱 |
| Docker Sandboxes | 實驗性容器 | Docker 官方方案 |
| Modal | 容器/VM | 雲端函式平台 |

## 參考

- [Northflank — AI Agent Sandboxing Guide](https://northflank.com/blog/how-to-sandbox-ai-agents)
- [Microsoft — Agent Governance Toolkit](https://opensource.microsoft.com/blog/2026/04/02/introducing-the-agent-governance-toolkit-open-source-runtime-security-for-ai-agents/)
- [Cloudflare — Dynamic Workers Beta](https://www.infoq.com/news/2026/04/cloudflare-dynamic-workers-beta/)
- [Elevate Consult — Zero Trust AI Agents](https://elevateconsult.com/insights/securing-autonomous-ai-agents-in-2026-what-every-business-needs-to-know/)
