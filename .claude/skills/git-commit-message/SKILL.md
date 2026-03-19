---
name: git-commit-message
description: >
  撰寫 Git commit 訊息的專用技能。當使用者要求「寫 commit 訊息」、「幫我 commit」、「產生 commit message」、「git commit」，或提供程式碼差異（diff）/變更摘要請 Claude 描述這次變更時，請務必啟用此技能。即使使用者只說「幫我描述這次改動」或「這次改了什麼」也應觸發此技能。適用於任何語言的專案、任何規模的 commit。
---

# Git Commit Message 撰寫指南

你的任務是根據使用者提供的 diff、變更摘要、或情境描述，產生一則高品質的 Git commit 訊息。

## 核心原則：商業語言優先

這是最重要的一條原則：**commit 訊息的讀者不只有工程師，也包含產品經理、業務、設計師等非技術人員。**

- 優先描述「這次改動對業務/使用者帶來什麼改變」，而非「程式碼做了什麼」
- 用「新增會員登入功能」而非「實作 JWT authentication middleware」
- 用「修正結帳流程無法完成的問題」而非「fix null pointer exception in CheckoutService」
- 只有當改動**純屬程式碼內部調整**（重構、效能優化、測試、CI 設定等），才允許使用工程語言描述

## 語言規則

- **繁體中文為主**：除了下列例外，所有內容一律使用繁體中文
- **保留英文的情況**：
  - Git Type（`feat`、`fix`、`docs` 等）
  - 程式碼、變數名、函式名（如 `handlePayment()`、`userId`）
  - 專有名詞、品牌名稱（如 `Stripe`、`OAuth`、`Redis`）
  - 技術協定與規格（如 `REST API`、`JWT`、`SQL`）

## Conventional Commits v1.0.0 格式

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Type 選用規則

| Type | 使用時機 |
|------|----------|
| `feat` | 新增功能（對外可見的行為改變） |
| `fix` | 修正錯誤或問題 |
| `docs` | 文件變更（README、說明文件等） |
| `style` | 格式調整，不影響邏輯（縮排、空格等） |
| `refactor` | 程式碼重構，不增加功能也不修 bug |
| `perf` | 效能改善 |
| `test` | 新增或修改測試 |
| `chore` | 維護性工作（依賴套件更新、設定檔調整等） |
| `build` | 建置系統或外部依賴變更 |
| `ci` | CI/CD 流程設定變更 |
| `revert` | 還原先前的 commit |

### Scope（範圍）

用小括號標示影響範圍，建議使用業務模組名稱而非技術層名稱：
- 好的 scope：`(訂單)`、`(會員)`、`(金流)`、`(報表)`
- 可接受：`(auth)`、`(api)`（若無法翻譯的技術範疇）
- 避免：`(database-layer)`、`(middleware-stack)`

### Description（標題描述）

- 用動詞開頭，描述**發生了什麼事**
- 限制在 72 字元以內（中文約 24 個字）
- 不加句號結尾
- 使用肯定句，不用被動語態

**範例比較：**

| 不好（工程導向） | 好（商業導向） |
|-----------------|----------------|
| `feat: implement user authentication` | `feat(會員): 新增會員登入與註冊功能` |
| `fix: resolve null pointer in order processing` | `fix(訂單): 修正訂單送出後畫面卡住的問題` |
| `refactor: extract payment service class` | `refactor(金流): 拆分金流邏輯，方便日後對接多家支付商` |

### Body（內文）

- 說明「為什麼要做這個改動」和「改動的影響範圍」
- 每行不超過 72 字元
- 與標題之間空一行
- 適用時機：改動複雜、影響範圍廣、或需要說明背景

### Footer（頁腳）

- `BREAKING CHANGE: <說明>` — 代表不向下相容的重大改動
- `Closes #<issue-number>` — 關聯 issue
- `Co-authored-by: <name> <email>` — 共同作者

## 輸出步驟

1. **分析變更** — 理解這次 diff/摘要的商業目的
2. **選擇 Type 和 Scope** — 從業務角度判斷
3. **撰寫標題** — 精簡、用商業語言
4. **判斷是否需要 Body** — 複雜改動才加
5. **輸出最終訊息** — 用 markdown code block 包裝，方便複製

## 完整範例

**情境**：在電商後台新增了一個讓客服人員可以手動退款給指定訂單的功能

```
feat(訂單): 新增客服人工退款功能

客服人員現在可以在後台針對個別訂單執行部分或全額退款，
退款金額將直接回到顧客原始付款方式，並自動發送通知信。

此功能需要「客服主管」以上的帳號權限才能操作。
```

---

**情境**：修正了一個報表匯出 Excel 時，日期欄位顯示錯誤的 bug

```
fix(報表): 修正匯出 Excel 時日期格式顯示異常

日期欄位原本輸出為 Unix timestamp 數字，現已修正為
正確的 YYYY-MM-DD 格式，確保匯出資料可直接閱讀。
```

---

**情境**：升級了 Node.js 版本和幾個 npm 套件

```
chore: 升級 Node.js 至 v20 並更新相關依賴套件
```
