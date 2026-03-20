# HiSKIO 廣告文案生成工具

使用 Claude Code + AI Skill，協助企劃人員依標準化流程產生符合品牌規範的廣告文案。

支援 FB 廣告、EDM（陌生開發 / 舊生 / 購物車再行銷）、粉專貼文，適用於 Vibe Coding、Claude Code、RAG 等所有 HiSKIO 課程。

---

## 使用前置條件

- 已安裝 [Claude Code](https://claude.ai/code) CLI
- 可以訪問 Github repository 權限

---

## 步驟一：安裝 Plugin

<video src="docs/安裝生成廣告%20Plugin.mp4" controls width="100%"></video>

---

## 步驟二：執行廣告文案撰寫

<video src="docs/介紹生成廣告%20Skill%20使用方式.mp4" controls width="100%"></video>

1. 在專案目錄下啟動 Claude Code：

   ```bash
   claude
   ```

2. 直接告訴 Claude 你想寫的廣告類型，Skill 會自動啟動。範例指令：

   ```
   幫我寫一篇 Vibe Coding 體驗課的 FB 廣告
   幫我寫一封 Claude Code 課程的 EDM
   幫我寫一篇 RAG 課程的粉專貼文
   ```

3. Claude 會引導你完成以下五個階段：

   | 階段    | 說明                         |
   | ------- | ---------------------------- |
   | Stage 1 | 素材確認（填寫文案問卷）     |
   | Stage 2 | 資訊搜集與確認               |
   | Stage 3 | AI 初稿生成                  |
   | Stage 4 | 微調協助（順稿）             |
   | Stage 5 | 儲存輸出至 `outputs/` 資料夾 |

4. 文案定稿後，檔案會自動儲存至 `outputs/<課程名稱>.md`。

---

## 專案結構

```
advertise/
├── docs/                          # 操作教學影片
│   ├── 安裝生成廣告 Plugin.mp4
│   └── 介紹生成廣告 Skill 使用方式.mp4
├── marketplace/
│   └── hiskio-ad-copywriter/      # Plugin 本體
│       ├── .claude-plugin/
│       │   └── plugin.json
│       └── skills/
│           └── hiskio-ad-copywriter/
│               ├── SKILL.md       # Skill 定義與流程
│               └── references/   # 品牌風格指南與文案範例
└── outputs/                       # 生成文案的輸出目錄（自動建立）
```

---

## 常見問題

**Q：Skill 沒有自動啟動？**
A：確認 Plugin 已正確安裝（`claude plugin list`），並重新啟動 Claude Code。

**Q：文案儲存在哪裡？**
A：儲存在專案根目錄的 `outputs/` 資料夾，檔名以課程名稱命名。

**Q：可以同時產生多個版本嗎？**
A：可以。在 Stage 4 微調時告知 Claude 你需要 A/B 版本，它會分別產出。
