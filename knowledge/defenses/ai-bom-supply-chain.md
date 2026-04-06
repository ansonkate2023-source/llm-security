# AI BOM 與供應鏈安全

**分類：** defense
**風險等級：** Critical
**最後更新：** 2026-04-06

## 概述

傳統 SBOM 已無法涵蓋 AI 原生系統的完整供應鏈風險。2026 年軟體供應鏈安全從「可見性時代」進入「治理時代」，從靜態 SBOM 過渡到 agentic 治理。AI 模型如同另一個第三方依賴項，但傳統掃描器無法讀取。

## AI-BOM（AI Bill of Materials）

### 定義
AI-BOM 是組織 AI 生態系統的完整清單，包含：
- AI 模型及其架構
- 訓練資料集與資料來源
- 嵌入向量（Embeddings）
- 編排層（Orchestration layers）
- 第三方 AI 服務
- 基礎設施依賴
- 以上各項之間的關係

### 與傳統 SBOM 的差異

| 維度 | SBOM | AI-BOM |
|------|------|--------|
| 涵蓋範圍 | 軟體套件、函式庫 | 模型、資料集、服務、基礎設施 |
| 風險類型 | 程式碼漏洞 | 模型偏見、投毒、RCE（pickle 格式）|
| 掃描工具 | 傳統 SCA | 專用 ML 安全掃描器 |
| 更新頻率 | 版本發布時 | 模型更新、資料變更時 |

### CycloneDX ML-BOM
- **標準：** Machine Learning Bill of Materials
- **功能：** 文件化訓練資料、架構決策、安全基準
- **來源：** [CycloneDX](https://cyclonedx.org/capabilities/mlbom/)

## 2026 供應鏈安全關鍵支柱

### 1. MLSecOps — 模型完整性
- 模型簽名與驗證
- 訓練資料溯源
- 模型行為監控

### 2. 二進制生命週期管理 — 製品溯源
- 建構可驗證性
- 簽名鏈完整性
- 部署追蹤

### 3. Agentic 修復 — 壓縮 MTTR
- 自動化漏洞修復
- AI 驅動的風險評估
- 即時補丁管理

## AI 模型特有風險

### Pickle 格式 RCE
- 許多 AI 模型以 pickle 格式分發
- 載入時允許遠端程式碼執行
- 傳統掃描器無法偵測

### 模型竊取與替換
- 攻擊者可替換模型權重
- 無完整性驗證機制時無法偵測

### 資料投毒
- 訓練資料被汙染
- AI-BOM 需追蹤資料來源

## 工具

### AIsbom
- **功能：** ML 製品的安全與合規掃描器
- **GitHub：** [Lab700xOrg/aisbom](https://github.com/Lab700xOrg/aisbom)

### 美國國防部指引
- 2026 年 3 月發布 AI/ML 供應鏈風險與緩解指引
- **來源：** [DoD PDF](https://media.defense.gov/2026/Mar/04/2003882809/-1/-1/0/AI_ML_SUPPLY_CHAIN_RISKS_AND_MITIGATIONS.PDF)

## 參考

- [Wiz — AI-BOM](https://www.wiz.io/academy/ai-security/ai-bom-ai-bill-of-materials)
- [SD Times — From SBOM to AI BOM](https://sdtimes.com/ai/from-sbom-to-ai-bom-rethinking-supply-chain-security-for-ai-native-software/)
- [Cloudsmith — 2026 Supply Chain Security Guide](https://cloudsmith.com/blog/the-2026-guide-to-software-supply-chain-security-from-static-sboms-to-agentic-governance)
- [CycloneDX — ML-BOM](https://cyclonedx.org/capabilities/mlbom/)
