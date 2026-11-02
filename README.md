# 故事工作室 Son's Story Studio

一個給孩子寫故事的小天地 — 單檔靜態網頁 App，可安裝到手機/平板主畫面。

## 功能
- 📚 故事書架：開新故事、章節管理
- ✍️ 寫作區：自動儲存，孩子自己寫
- 💡 靈感按鈕：AI 只給提示點子，從不代筆（按一下才觸發）
- 🎨 AI 插圖：Pollinations.ai 免費生成
- 🃏 角色卡：上載照片、編輯角色
- 💾 備份/還原：JSON 匯出匯入

## 安裝成 App
用 Chrome / Safari 開啟 GitHub Pages 網址 → 「加到主畫面」，
就會有獨立 icon，可以全螢幕使用，離線都開得返。

## 技術
- 單一 `index.html`，無 build 步驟
- PWA：`manifest.json` + `sw.js` 離線快取
- 資料存在瀏覽器 localStorage
