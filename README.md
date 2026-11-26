# RUBY Smart Chip — GitHub Pages Edition

這是一個不需要 Telegram Bot 或後端主機的本機籌碼計算工具。網站使用 GitHub Pages 託管 HTML 與 JavaScript，並使用 Pyodide 在瀏覽器內執行來自 RUBY TG Chip V1.8.18 的 26 套策略計算核心。

## 功能

- 手機及電腦響應式操作介面，冰綠／冰藍主題
- 26 套策略搜尋、介紹、參數設定
- 每碼注碼、總注、局數、關卡、可用金額與盈虧
- 手動中／掛計算、上一局更正、每組局數完成後自動切換下一組進度（#1 → #2 → #3）
- #26 等分倍盈歸本的歸本／鎖利規則
- 最近紀錄、本機歷史封存、JSON 備份與還原、CSV 匯出
- 進度換組保留累計盈虧和原策略關卡；停損、停利、策略末關及資金不足仍可暫停
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

V0.1.3 已於 GitHub 獨立測試分支執行 Python 3.13 回歸：26 套策略的中、掛、上一局撤銷、重新載入；全部 26 套策略模擬第 34→35 局的換組邊界；#09、#18 各連續結算 71 局；跨組撤銷與重新執行、舊版 35/35 紀錄恢復、#07 冷卻暫停／恢復，合計 **539 項檢查通過**。另以 Playwright Chromium 手機尺寸透過 Pyodide 實際點選 35 次「中」，確認進入 #2 且中／掛可用、撤銷、重載及 #07 暫停／恢復流程通過。這是測試環境驗收，尚未在使用者的 iPhone 或正式 GitHub Pages 上完成驗證。

V0.1.3 僅提交到修正分支，未合併 `main`、未部署正式 GitHub Pages，也尚未在真實手機網路環境完成 Pyodide 全流程驗收。若遇到首次載入失敗，先檢查 jsDelivr CDN 能否連線，而不是重裝 Python。
