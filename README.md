# 元太科技 8069 即時股價

單一 `index.html` 的靜態網頁，可直接放在 GitHub Pages。

## 部署到 GitHub Pages

1. 在 GitHub 建立新的 repository（例如 `eink-stock`），設為 Public。
2. 把 `index.html`（和這份 README）上傳到 repo 根目錄：
   - 網頁操作：repo 頁面 → **Add file → Upload files** → 拖入檔案 → Commit。
   - 或用指令：
     ```bash
     git init && git add . && git commit -m "init"
     git branch -M main
     git remote add origin https://github.com/<你的帳號>/eink-stock.git
     git push -u origin main
     ```
3. repo → **Settings → Pages** → Source 選 **Deploy from a branch**，Branch 選 `main`、資料夾 `/ (root)` → Save。
4. 約 1 分鐘後網址會是 `https://<你的帳號>.github.io/eink-stock/`。

## 運作方式

- 主要資料：臺灣證券交易所 MIS 即時報價（`otc_8069.tw`）。
- 備援：Yahoo Finance（`8069.TWO`），同時用來畫今日走勢圖。
- 因為 GitHub Pages 是純靜態網站，瀏覽器無法直接跨網域呼叫這些 API，所以透過公開 CORS 代理（allorigins、corsproxy.io、codetabs）依序嘗試。若某個代理掛掉會自動換下一個。
- 「更新」按鈕立即重抓；勾選「自動更新」則在台股盤中（週一至五 09:00–13:30）每 30 秒更新。

要改成其他股票，修改 `index.html` 中的 `SYMBOL`（上市股票需把 `otc_` 改成 `tse_`、`.TWO` 改成 `.TW`）。
