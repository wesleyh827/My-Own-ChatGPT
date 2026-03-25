# 本地 AI 助理

一個基於 [Ollama](https://ollama.com) 的本地端 AI 聊天網頁，所有對話完全在電腦上處理，不需要 API Key，不需要網路，資料不會離開電腦。

---

## 功能特色

- **Word Streaming**：AI 回應逐字顯示，就像 ChatGPT 一樣
- **多輪對話記憶**：每次送出都帶上完整的對話歷史
- **對話記錄側欄**：可開新對話、切換對話、刪除對話，重新整理後也不會消失
- **選擇模型**：自動偵測已安裝的 Ollama 模型，右上角下拉切換
- **Markdown 渲染**：支援標題、粗體、清單、表格、程式碼高亮
- **程式碼一鍵複製**：程式碼區塊右上角有複製按鈕
- **連線狀態指示**：左上角綠燈／紅燈顯示 Ollama 是否在線
- **完全本地端**：不需要後端伺服器，單一 HTML 檔案即可執行

---

## 安裝與使用

### 第一步：安裝 Ollama

前往 [https://ollama.com](https://ollama.com) 下載並安裝。

### 第二步：下載模型

```bash
ollama pull llama3.2
```

> 建議也可以安裝對繁體中文支援更好的 `qwen2.5`：
> ```bash
> ollama pull qwen2.5
> ```

### 第三步：啟動 Ollama（允許網頁存取）

```bash
# Mac / Linux
OLLAMA_ORIGINS="*" ollama serve

# Windows
set OLLAMA_ORIGINS=*
ollama serve
```

> 如果出現 `address already in use` 錯誤，表示 Ollama 已經在背景執行。
> 請先關閉再重新啟動：
> ```bash
> pkill ollama
> OLLAMA_ORIGINS="*" ollama serve
> ```

### 第四步：啟動本地伺服器

在 `ollama-chat.html` 所在的資料夾執行：

```bash
python3 -m http.server 8080
```

### 第五步：開啟網頁

用瀏覽器前往：

```
http://localhost:8080/chatgpt-clone.html
```

---

## 檔案結構

```
.
└── chatgpt-clone.html   # 主程式（單一檔案，包含所有 HTML / CSS / JS）
```

---

## 使用技術

| 技術 | 用途 |
|------|------|
| HTML / CSS / JavaScript | 前端介面 |
| [Ollama](https://ollama.com) | 本地 LLM 推理引擎 |
| [marked.js](https://marked.js.org) | Markdown 渲染 |
| [highlight.js](https://highlightjs.org) | 程式碼語法高亮 |
| localStorage | 對話記錄本地儲存 |

---

## 常見問題

**Q：左上角一直是紅燈？**
確認已執行 `OLLAMA_ORIGINS="*" ollama serve`，且沒有用直接點兩下開 HTML（要透過 `http://localhost:8080`）。

**Q：回應是簡體中文？**
切換到 `qwen2.5` 模型，對繁體中文的支援比 llama 好很多。
