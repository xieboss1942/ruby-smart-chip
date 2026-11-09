# RUBY Smart Chip — GitHub Pages Edition

這是一個不需要 Telegram Bot 或後端主機的本機籌碼計算工具。網站使用 GitHub Pages 託管 HTML 與 JavaScript，並使用 Pyodide 在瀏覽器內執行來自 RUBY TG Chip V1.8.18 的 26 套策略計算核心。

## 功能

- 手機及電腦響應式操作介面，冰綠／冰藍主題
- 26 套策略搜尋、介紹、參數設定
- 每碼注碼、總注、局數、關卡、可用金額與盈虧
- 手動中／掛計算、上一局更正、局數硬性上限
- #26 等分倍盈歸本的歸本／鎖利規則
- 最近紀錄、本機歷史封存、JSON 備份與還原、CSV 匯出
- 不使用 BOT_TOKEN、不送真實注單、不讀取交易平台資料

## 最簡單部署：單檔版

1. 在 GitHub 登入並進入 **https://github.com/new**。
2. **Repository name** 輸入 `ruby-smart-chip`。
3. 選擇 **Public**（GitHub Free 的 Pages 通常需要公開儲存庫），其他保持預設，點 **Create repository**。
4. 在新的儲存庫按 **Add file → Upload files**。
5. 從單檔版 ZIP 解壓，將其中的 `index.html` 上傳到儲存庫最上層，按 **Commit changes**。
6. 進入 **Settings → Pages → Build and deployment**，`Source` 選 `Deploy from a branch`，`Branch` 選 `main` 和 `/(root)`，再按 **Save**。
7. 等 GitHub Pages 顯示已發布的正式網址後，從該網址開啟網站。

不需要自訂網址、雲端資料庫、Python 伺服器或 Telegram Token。**首次載入網頁需要連網下載 Pyodide 計算執行環境**，手機初次載入可能較慢。

## 其他部署方法：開發原始碼包

直接將 `index.html`、`styles.css`、`app.js`、`engine/`、`data/`、`.nojekyll` 上傳到儲存庫。這份是分檔版，方便未來改 UI 和策略。

## 安全與隱私

- GitHub Pages 站點內容與上傳的程式碼都可能公開。**請不要上傳 `BOT_TOKEN.txt`、`.env`、`data/users.json`、會員帳目或任何 Credential。**
- 由於 GitHub Pages 是靜態網站，配注演算法會送到使用者瀏覽器執行，因此訪客可以查看前端程式及其包含的計算邏輯。不適合直接公開商業機密演算法。
- 會員的試算紀錄放在自己的瀏覽器 `localStorage`。清除網站資料、使用無痕模式或換裝置，可能失去紀錄；請定期匯出 JSON。
- 這是模擬計算器，不會執行任何下注或自動交易。策略不能提高開獎命中機率，也不能保證獲利。

## 測試界線

已用原生 Python 測試：26 套策略載入、可報價策略的金額基本不變式、#26 六關等額、完成局數限制、上一局更正、100% 歸本。HTML、CSS 與 JavaScript 已做靜態檢查。

尚未在 GitHub Pages 實際部署或在真實手機網路環境完成 Pyodide 全流程驗收。若遇到首次載入失敗，先檢查 jsDelivr CDN 能否連線，而不是重裝 Python。
