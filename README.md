# 動態 MPT 資產配置回測平台 — GitHub Pages 部署說明

這個資料夾就是要上傳到新 GitHub repo 的全部內容：

```
index.html                  ← 回測平台本體（開啟網站看到的頁面）
multi_strategy_data.xlsx    ← 預設資料（網站開啟時會自動載入這份檔案）
```

網頁載入時會自動用瀏覽器的 `fetch()` 去讀取**同一個資料夾**裡檔名完全是
`multi_strategy_data.xlsx` 的檔案，自動解析、自動把所有策略/Benchmark 加入
清單並能直接按「執行回測」。側欄的「📤 上傳 / 更換 Excel」小按鈕保留著，用來
**暫時**換一份資料測試用；重新整理頁面就會還原成預設資料，不會動到 repo 裡的
檔案。

---

## 一、第一次部署（全程網頁操作，不需要裝 git）

1. 登入 GitHub → 右上角「+」→ **New repository**。
   - Repository name 自訂，例如 `mpt-allocation-backtester`
   - Public（GitHub Pages 的免費方案需要 Public repo，除非你有 GitHub Pro/Team）
   - 其他選項保持預設，直接 **Create repository**
2. 進入剛建立的空 repo 頁面，點 **uploading an existing file**（或 Add file →
   Upload files）。
3. 把這個資料夾裡的 `index.html` 和 `multi_strategy_data.xlsx` **兩個檔案一起**
   拖進去上傳（檔名、大小寫都不要改），下方填寫 commit 訊息，按
   **Commit changes**。
4. 進入 repo 的 **Settings** → 左側選單 **Pages**。
5. 「Build and deployment」→ Source 選 **Deploy from a branch**；
   Branch 選 **main**，資料夾選 **/(root)**，按 **Save**。
6. 等 1～2 分鐘，重新整理這個 Pages 設定頁，上方會出現網站網址，格式是：
   `https://<你的帳號>.github.io/<repo名稱>/`
   點進去就是可以分享給別人看的正式網址。

---

## 二、之後要更新「預設資料」

不用改任何程式碼，只要在 GitHub 網頁上把 `multi_strategy_data.xlsx` 換成新版本：

1. 打開 repo，點進 `multi_strategy_data.xlsx` 這個檔案。
2. 右上角垃圾桶旁邊有個鉛筆/上傳圖示，或直接回到 repo 根目錄按
   **Add file → Upload files**，把新的 Excel 檔案拖進去（**檔名務必維持
   `multi_strategy_data.xlsx`，不能改名**，否則網站會抓不到它）。
3. 上傳後 GitHub 會提示「這個檔案已存在，是否取代」，確認取代即可，再按
   **Commit changes**。
4. 等 1～3 分鐘讓 GitHub Pages 重新部署（GitHub 的 CDN 偶爾會快取舊檔案，
   如果重新整理網頁後資料還是舊的，可以強制重新整理：
   Windows/Linux 按 `Ctrl+Shift+R`，Mac 按 `Cmd+Shift+R`）。
5. 之後任何人打開網站網址，看到的都會是這份新資料 — 不需要每個人自己手動上傳。

> Excel 內部結構需維持「Strategies」「Benchmarks」兩個工作表名稱，
> 第一欄為日期、其餘欄位為各策略/Benchmark 的日報酬率，和目前這份檔案的格式一致即可。

---

## 三、側欄「上傳 / 更換 Excel」小按鈕的用途

這個按鈕 **不會** 改到 GitHub 上的預設資料，只在你當下瀏覽器分頁裡暫時替換，
適合用來：

- 測試還沒確定要不要正式換上去的新版資料
- 跟朋友/自己做臨時的一次性回測，不想動到正式網站的預設資料

重新整理頁面（或別人重新打開這個網址）就會自動變回讀取 repo 裡的
`multi_strategy_data.xlsx`。想讓所有訪客都看到新資料，請用上面「二、更新預設資料」
的方法正式取代檔案。

---

## 四、常見問題

**Q: 打開網站一直顯示「尚未載入（請上傳 .xlsx）」？**
A: 通常是 `multi_strategy_data.xlsx` 沒有跟 `index.html` 放在同一層資料夾，
或檔名打錯字／大小寫不同（GitHub Pages 的伺服器對檔名大小寫敏感）。回到 repo
確認根目錄裡兩個檔案都在，檔名完全是 `index.html` 與 `multi_strategy_data.xlsx`。

**Q: 可以用自訂網域嗎？**
A: 可以，在同一個 Settings → Pages 頁面的 Custom domain 欄位設定，並依指示
到你的網域商那邊加一筆 DNS 紀錄即可，之後網站網址就會變成你的網域。
