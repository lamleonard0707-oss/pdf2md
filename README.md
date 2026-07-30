# PDF → Markdown（慳返你部 AI 嘅額度）

一個單檔網頁：拖份 PDF 入去 → 即刻出乾淨 Markdown → 自動幫你複製好。

**做嘢全程喺你部機（瀏覽器）進行，份檔唔會上傳去任何伺服器。**

## 點解要轉

AI 讀 PDF 唔係「讀」——佢會將**每一頁 render 成一張圖片**，再連埋嗰頁文字一齊送入去。
所以一份 20 頁嘅嘢，你一句都未問，已經燒咗成 5 萬 token。

轉成文字之後 AI 一樣睇得到全部內容，但唔使再「影相」。

### 實測（20 頁中文 PDF，US Letter）

| | Token |
|---|---|
| 直接掉原本份 PDF | ≈ 59,070 |
| └ 其中「影相」部分 | ≈ 50,660（2,533 × 20 頁）|
| 轉完 Markdown | ≈ 8,410 |
| **慳** | **≈ 86%** |

慳嘅係「唔使影相」，**唔係**「執靚咗格式」——所以連純複製貼上都慳到。

## ⚠️ 幾時唔應該轉

如果你本身就想 AI 睇圖表、設計稿、掃描件 → **用原檔**。
因為慳到嗰 86% 正正就係啲圖，轉完 AI 就睇唔到。

## 技術

- [pdf.js](https://mozilla.github.io/pdf.js/) 抽文字（連字級、粗體、座標）
- 自己寫嘅版面還原：標題分級、段落合併、清頁首頁尾頁碼、欄位聚類還原表格
- Token 估算：文字 CJK ≈ 1.14/字、其餘 ≈ 1/4 字元；圖片用 Anthropic 公式 `(闊×高)/750`，最長邊 render 成 1568px
- 冇 build step、冇後端、冇追蹤

## 想要真·全自動（唔使開網頁）

用 Claude Code / Cursor 呢啲 AI Agent 嘅話，裝一次 MCP 就得：

```bash
pip install markitdown-mcp
claude mcp add markitdown -- markitdown-mcp
```

之後直接同個 Agent 講「幫我讀 ~/Downloads/報告.pdf」，佢自己識轉。

---

[@ll_station_ll](https://www.instagram.com/ll_station_ll/) · LL Station
