# 語音翻譯會議紀錄 PWA

一個純前端、可安裝到手機的網頁版會議紀錄工具。即時語音辨識 + 多語翻譯 + 一鍵匯出。

## 功能

- **語音辨識**：中文（繁體）、台語（實驗性）、英文、日文、韓文、簡中
- **即時多語翻譯**：可同時翻譯成多達 8 種目標語言
- **時間戳記**：每段發言自動記錄會議時間與絕對時間
- **暫停／繼續**：開會中接電話也不會中斷紀錄
- **匯出**：txt / Markdown / HTML 三種格式，或直接複製到剪貼簿
- **PWA**：可「加到主畫面」，像 App 一樣全螢幕使用，離線也能開啟頁面
- **保持螢幕不休眠**：錄音中自動 Wake Lock

---

## 部署到 GitHub Pages（免費、永久 HTTPS 網址）

> **為什麼一定要 HTTPS？** 瀏覽器規定：麥克風只能在 HTTPS 或 localhost 下使用。GitHub Pages 自動提供 HTTPS。

### 步驟一：建立 GitHub 帳號（如果還沒有）

到 <https://github.com> 註冊一個免費帳號。

### 步驟二：新增 Repository

1. 登入後點右上角 **+** → **New repository**
2. **Repository name** 填：`meeting-translator`（或你喜歡的名字）
3. 選 **Public**（Pages 免費版需要 Public）
4. **不要**勾選 "Add a README"
5. 按 **Create repository**

### 步驟三：上傳檔案

最簡單的方式是用網頁直接上傳：

1. 在剛建立的 repo 頁面，點 **uploading an existing file** 連結
2. 把這個資料夾裡的所有檔案拖進去：
   - `index.html`
   - `manifest.webmanifest`
   - `sw.js`
   - `icons/`（整個資料夾）
   - `README.md`
3. 下方按 **Commit changes**

### 步驟四：開啟 GitHub Pages

1. 在 repo 頁面點上方 **Settings**
2. 左側選單點 **Pages**
3. **Source** 選 **Deploy from a branch**
4. **Branch** 選 `main`，資料夾選 `/ (root)`
5. 按 **Save**
6. 等 1–2 分鐘，頁面上方會顯示你的網址，類似：
   `https://你的帳號.github.io/meeting-translator/`

### 步驟五：在手機上開啟並安裝

1. 用手機瀏覽器（**Chrome / Safari / Edge**）打開上面的網址
2. **Android Chrome**：會自動跳出「安裝」提示，或點瀏覽器選單 → 「加到主畫面」
3. **iPhone Safari**：點下方分享按鈕 → 「加入主畫面」
4. 主畫面會多一個 App 圖示，點開就是全螢幕的會議翻譯工具

---

## 替代部署方式

### Netlify Drop（不用註冊，30 秒上線）

1. 把整個 `meeting-translator-pwa` 資料夾壓縮成 `.zip`，或直接拖整個資料夾
2. 到 <https://app.netlify.com/drop>
3. 把資料夾拖進去
4. 立刻拿到一個 `xxx.netlify.app` 網址

### Cloudflare Pages

1. 到 <https://pages.cloudflare.com>
2. 用 GitHub 帳號連結，選擇 repo
3. Build 設定都留空，按部署即可

---

## 在區域網路內測試（不上網也能用）

如果只是要在自家 Wi-Fi 內測試（電腦當伺服器、手機連線使用），可以這樣做：

```bash
cd meeting-translator-pwa
python3 -m http.server 8000
```

電腦會顯示類似 `http://192.168.0.10:8000` 的網址，手機連同一個 Wi-Fi 就能打開。

⚠️ 但這樣是 HTTP 不是 HTTPS，**手機瀏覽器不會給麥克風權限**。所以這方法只能在電腦上測試介面，要實際錄音請用 GitHub Pages。

---

## 注意事項

- **台語（nan-TW）** 瀏覽器原生支援度有限，許多裝置會回傳 `language-not-supported`。建議改用「中文（繁體・台灣）」，多數台灣腔華語都能辨識。
- **翻譯 API**：使用 [MyMemory](https://mymemory.translated.net/) 免費版，每天每 IP 約 5,000 字額度。長時間會議建議分段使用。
- **隱私**：語音辨識在瀏覽器本地處理，不會上傳音訊；只有辨識完成後的文字才會送到翻譯 API。
- **不支援的瀏覽器**：Firefox 桌面版尚未實作 Web Speech API。請用 Chrome / Edge / Safari。

---

## 檔案結構

```
meeting-translator-pwa/
├── index.html              # 主應用
├── manifest.webmanifest    # PWA 中繼資料
├── sw.js                   # Service Worker（離線快取）
├── icons/
│   └── icon.svg            # App 圖示
└── README.md               # 本檔案
```
