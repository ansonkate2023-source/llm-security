# Unicode 隱形攻擊（Invisible Unicode Attacks）

**分類：** attack
**風險等級：** High
**最後更新：** 2026-04-06

## 概述

隱形墨水攻擊（Invisible Ink Attacks）是一種精密的間接 prompt injection 形式。利用不可渲染的 Unicode 字元在看似無害的文字中嵌入隱藏指令 — 人類看到無害訊息，而 AI 模型看到詳細的惡意指令。

## 攻擊技術

### 1. Unicode 變體選擇器利用（Variation Selector Exploitation）
- Unicode 變體選擇器（VS）：256 個碼點（U+FE00-U+FE0F, U+E0100-U+E01EF）
- 三大有效特性：
  - **視覺隱身** — 設計為非間距且不可見
  - **高熵** — 分解高範圍 VS 字元產生長序列的「垃圾」token，干擾注意力機制
  - **梯度流** — 作為有效 Unicode 允許有效梯度計算

### 2. Tag 字元隱形編碼
- 將原始 Unicode 碼點加上 E0000 範圍（E0000 至 E007F）
- 英文字母、數字、標點符號可被「標記」為不可見
- 僅需幾行程式碼即可使 prompt 隱形
- LLM 在 token/字元層級正常處理這些字元

### 3. 零寬度字元注入
- 零寬度空白（U+200B）
- 零寬度非斷行（U+FEFF）
- 零寬度連接符（U+200D）

## 真實世界攻擊（2026）

### Glassworm 攻擊
- **日期：** 2026-03-12
- **受害：** npm 套件（@aifabrix/miso-client、@iflow-mcp/watercrawl-watercrawl-mcp）
- **受害：** VS Code 擴充（quartz.quartz-markdown-editor）
- **攻擊方式：** 使用不可見 Unicode 字元隱藏惡意 payload
- **來源：** [DEV Community — Glassworm](https://dev.to/ohmygod/glassworm-how-invisible-unicode-characters-and-solana-are-powering-the-biggest-supply-chain-attack-4a4j)

### Reverse CAPTCHA 研究
- 評估 LLM 對不可見 Unicode 指令注入的易受性
- **來源：** [arXiv](https://arxiv.org/html/2603.00164v1)

## 影響範圍

- 所有處理文字輸入的 LLM 應用
- RAG 系統（隱藏在文件中的指令）
- 電子郵件 AI 助理
- 程式碼審查 AI 工具
- npm/PyPI 套件（供應鏈攻擊）

## 防禦策略

### AWS 建議
- Amazon 發布專門的 Unicode 字元走私防禦指南
- **來源：** [AWS Security Blog](https://aws.amazon.com/blogs/security/defending-llm-applications-against-unicode-character-smuggling/)

### 具體措施
1. **Unicode 正規化** — 在處理前移除不可見/控制字元
2. **輸入清理** — 過濾已知的隱形 Unicode 範圍
3. **可見性驗證** — 確認輸入中的所有字元都可渲染
4. **Token 分析** — 監控異常的 token 模式
5. **套件掃描** — 掃描依賴項中的隱藏 Unicode payload

## 參考

- [TheHGTech — Unicode LLM Attacks](https://thehgtech.com/guides/unicode-llm-attacks.html)
- [TheHGTech — Advanced Unicode Attacks](https://thehgtech.com/guides/unicode-llm-attacks-advanced.html)
- [AWS — Unicode Character Smuggling Defense](https://aws.amazon.com/blogs/security/defending-llm-applications-against-unicode-character-smuggling/)
- [Prompt Security — Unicode Exploits](https://prompt.security/blog/unicode-exploits-are-compromising-application-security)
- [Technology.org — Invisible Unicode Malicious Code](https://www.technology.org/2026/03/16/hackers-are-hiding-malicious-code-in-plain-sight-using-invisible-unicode-characters/)
