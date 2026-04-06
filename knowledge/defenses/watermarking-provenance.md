# AI 水印與內容溯源（Watermarking & Provenance）

**分類：** defense
**風險等級：** High
**最後更新：** 2026-04-06

## 概述

2026 年成為隱寫術水印（steganographic watermarking）元年。EU AI Act 透明度要求於 2026-08 全面生效，專業創作者須確保 AI 生成影片帶有可見標籤與機器可讀元資料。C2PA 標準持續演進但仍面臨社群媒體分享時元資料被剝離的挑戰。

## C2PA（Coalition for Content Provenance and Authenticity）

### 技術規格
C2PA 規格整合以下技術：
- **元資料嵌入** — 可見與不可見
- **水印技術** — 隱寫術水印
- **密碼學簽名** — 數位內容簽章
- **數位指紋** — 內容指紋標記

### 2026 年進展
- Samsung Galaxy S25 首次在消費級手機原生相機中整合 C2PA 簽名
- 歐盟實踐守則建議多層方法：元資料嵌入 + 不可察覺水印 + 日誌記錄
- Cloudflare 探索密碼學水印方案

### 已知限制
- 大多數社群媒體平台重壓縮/重格式化上傳影像，剝離 C2PA 元資料
- 需要多層防護而非依賴單一機制
- 去除水印的攻擊技術持續演進

## 模型指紋（Model Fingerprinting）

### 用途
- 偵測被竊取/複製的模型
- 追蹤模型來源
- 使模型竊取可被起訴

### 2026 年影響
- 根本改變模型竊取的經濟學
- 攻擊者不再能無後果地萃取模型
- 複製品可被偵測、追蹤和起訴

## AI 內容水印

### 隱寫術水印（Steganographic Watermarking）
- 將資料隱藏在像素中
- 即使影片被重新編碼或跨平台分享仍然存在
- 幾乎不可能移除
- 2026 年主流技術

### 文字水印
- 在 LLM 輸出中嵌入統計不可見的模式
- 用於識別 AI 生成的文字
- 持續的研究領域

## 法規要求

| 法規 | 要求 | 生效日期 |
|------|------|----------|
| EU AI Act | AI 生成影片須帶可見標籤 + 機器可讀元資料 | 2026-08 |
| EU Code of Practice | 多層方法：元資料 + 水印 + 日誌 | 進行中 |
| 全球趨勢 | AI 影片水印強制要求持續擴大 | 2026+ |

## 參考

- [C2PA Specification](https://spec.c2pa.org/specifications/specifications/2.2/explainer/_attachments/Explainer.pdf)
- [AI Competence — C2PA and AI Supply Chain](https://aicompetence.org/c2pa-ai-supply-chain-verifying-authenticity/)
- [Cloudflare — Cryptographic Watermarks](https://blog.cloudflare.com/an-early-look-at-cryptographic-watermarks-for-ai-generated-content/)
- [Magiclight — C2PA Global Mandates 2026](https://magiclight.ai/news/c2pa-and-global-watermarking-mandates-for-ai-video-in-2026/)
- [Google — Gen AI Content Transparency](https://blog.google/technology/ai/google-gen-ai-content-transparency-c2pa/)
