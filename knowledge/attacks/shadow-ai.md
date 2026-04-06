# Shadow AI 風險

**分類：** attack
**風險等級：** High
**最後更新：** 2026-04-06

## 概述

Shadow AI 指員工未經授權在工作流程中使用 AI 工具。2026 年影響超過 75% 的企業，41% 員工承認未經批准使用 LLM。Shadow AI 為平均資料洩露成本增加 $670,000。

## 規模與影響

| 指標 | 數據 |
|------|------|
| 受影響企業 | 75%+（Cisco/UpGuard） |
| 未授權 LLM 使用員工 | 41% |
| 將資料貼入 GenAI prompt | 77% |
| 使用非企業帳號操作 | 82% |
| Shadow AI 導致的資料洩露 | 20% 企業 |
| 具偵測/治理政策的企業 | 僅 37% |
| 平均增加的洩露成本 | $670,000 |

## 常見形式

1. **瀏覽器公共 LLM** — ChatGPT、Claude 等公開服務
2. **本地模型執行** — Ollama、Llama.cpp 等本地推理
3. **流氓瀏覽器擴充** — 未經審查的 AI 擴充套件
4. **自建 Agent 框架** — 自製 MCP 工具、Clawdbot 變體
5. **第三方 AI 整合** — 未經 IT 批准的 SaaS AI 功能

## 核心風險

### 資料洩露
- 員工將機密資料、程式碼、客戶資訊貼入公共 LLM
- 資料可能被用於模型訓練
- 非企業帳號無法追蹤或審計

### 合規違規
- **GDPR** — 需要法律依據處理個人資料並能刪除
- **HIPAA** — 嚴格控制病患資料
- 未授權工具破壞所有安全保障

### 不可追蹤決策
- AI 輔助的決策無法被審計
- 無法確認哪些業務決策受 AI 影響
- 出錯時無法追溯原因

### 品質與準確性
- 員工可能依賴未驗證的 AI 輸出
- 幻覺風險無人監控
- 無安全護欄

## 防禦策略

### 偵測
- 網路流量監控（識別 AI API 呼叫）
- 端點 DLP（偵測敏感資料傳送至 AI 服務）
- 瀏覽器安全策略

### 治理
- 建立企業 AI 使用政策
- 提供批准的 AI 工具替代方案
- AI 使用培訓與意識提升

### 技術控制
- API 閘道與存取控制
- 資料分類標記
- AI 代理平台（將使用導向受控環境）

## 參考

- [Lasso Security — What is Shadow AI](https://www.lasso.security/blog/what-is-shadow-ai)
- [ByteVanguard — Shadow AI Rogue LLMs 2026](https://bytevanguard.com/2026/02/03/shadow-ai-rogue-llms-risk-2026/)
- [Palo Alto Networks — Shadow AI](https://www.paloaltonetworks.com/cyberpedia/what-is-shadow-ai)
- [Netwrix — 12 Shadow AI Security Risks](https://netwrix.com/en/resources/blog/shadow-ai-security-risks/)
- [Invicti — Shadow AI Risks 2026](https://www.invicti.com/blog/web-security/shadow-ai-risks-challenges-solutions-for)
