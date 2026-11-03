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
- ☁️ 跨裝置同步：Firebase Firestore（免費 Spark plan），同步碼配對，免登入

## 跨裝置同步設定（做一次）
1. 去 console.firebase.google.com → Add project（改名例如 `son-story-studio`，唔使開 Analytics）→ Create。
   留喺預設嘅 **Spark plan**（免費，唔使綁卡，**唔好 upgrade 去 Blaze**）。
2. 左邊 Build → **Firestore Database** → Create database → Start in **production mode**
   → Location 揀 `asia-east2 (Hong Kong)` → Enable。
3. Firestore Database → **Rules**，貼入以下內容 → Publish：
   ```
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /storyStudio/{code}/{doc=**} {
         allow read, write: if code.matches('^[A-Z2-9]{8}$');
       }
     }
   }
   ```
4. 左邊 Build → **Authentication** → Get started → Sign-in method → **Anonymous** → Enable → Save。
5. 左上角 Project Overview → `</>` (Add Web app) → 隨便改個名 → Register app
   → 將 `firebaseConfig` 嗰幾行貼入 `index.html` 頂部嘅 `FIREBASE_CONFIG`（取代「未設定」），push 上 GitHub。
6. 喺 iPhone 開 App → 故事架最底「☁️ 跨裝置同步」→ **開新同步碼** → 喺 iPad 輸入同一個碼。
   之後兩部機自動同步（約 2 秒）。唔用嗰陣撳「停用」就得。

注意：apiKey 直接擺喺網頁係正常做法（Firebase 官方都係咁），安全靠第 3 步嘅 Rules；
同步碼係 8 位隨機碼，估唔到就讀唔到你啲故事。
