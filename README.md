# 像素小鎮：放上 GitHub 嘅步驟

朋友打開網站，輸入邀請碼就入到，唔使註冊任何帳戶。
資料存喺 Firebase（Google 嘅免費資料庫），網站本身放喺 GitHub Pages。

**你嘅邀請碼：`TOWN-GX7PC`**（可以喺第 1 部分第 4 步改）

資料夾入面有：

| 檔案 | 用途 |
|---|---|
| `index.html` | 遊戲本身 |
| `firebase-config.js` | 等你貼 Firebase 設定落去 |
| `firestore.rules` | 資料庫保安規則，包括邀請碼 |

---

## 第 1 部分：開 Firebase（大約 10 分鐘）

1. 去 https://console.firebase.google.com ，用 Google 帳戶登入，撳 **建立專案**（Create a project）。改個名例如 `pixel-town`。Google Analytics 可以關咗佢。
2. 開匿名登入：左邊 **Build → Authentication → Get started → Sign-in method**，揀 **Anonymous（匿名）**，開咗佢再儲存。
   朋友唔使註冊，就係靠呢個功能。
3. 開資料庫：左邊 **Build → Firestore Database → Create database**。
   - 位置揀 `asia-east2 (Hong Kong)`，揀好之後改唔到
   - 模式揀 **Production mode**
4. 設定保安規則：喺 Firestore 入面撳 **Rules（規則）** 分頁，刪晒入面原本嘅內容，再貼上 `firestore.rules` 嘅全部內容，然後撳 **Publish（發布）**。
   - 想改邀請碼，就改 `return "TOWN-GX7PC";` 嗰行。輸入時唔分大細楷，但規則入面要用**大楷**
5. 攞網站設定：撳左上角齒輪 **Project settings（專案設定）**，向下碌到 **Your apps**，撳 `</>`（Web）圖示，改個名再撳 Register。
   畫面會顯示一段 `const firebaseConfig = { apiKey: ..., ... }`。
6. 用記事本打開 `firebase-config.js`，將 `{ ... }` 成段換成你啱啱攞到嗰段，然後儲存。

## 第 2 部分：放上 GitHub（大約 5 分鐘）

1. 登入 https://github.com ，撳右上角 **＋ → New repository**。
   - 名：`pixel-town`
   - 揀 **Public**（免費帳戶要用 Public 先開到 GitHub Pages）
   - 撳 **Create repository**
2. 喺新 repo 嘅頁面撳 **uploading an existing file**，將 `index.html`、`firebase-config.js`、`firestore.rules`、`README.md` 拖入去，再撳 **Commit changes**。
3. 撳 **Settings → Pages**。Source 揀 **Deploy from a branch**，Branch 揀 `main`、`/ (root)`，撳 **Save**。
4. 等一至兩分鐘，網站就會喺呢度：
   `https://你嘅GitHub名.github.io/pixel-town/`
5. 返去 Firebase，喺 **Authentication → Settings → Authorized domains** 撳 **Add domain**，加入 `你嘅GitHub名.github.io`。

## 第 3 部分：邀請朋友

將網站連結同邀請碼傳俾朋友就得。

---

## 常見問題

**apiKey 公開咗會唔會唔安全？**
唔會。Firebase 嘅網頁設定本身就係設計嚟公開。真正保護資料嘅係 Firestore 規則，未輸入啱邀請碼嘅人乜都睇唔到、改唔到。

**點樣踢走一個人？**
Firestore 入面有個 `members` 集合，刪走嗰個人嘅文件就得。佢個角色喺 `residents` 入面，都可以一齊刪。之後記得改埋邀請碼。

**朋友換咗手機點算？**
角色記喺瀏覽器度。換機、換瀏覽器或者清咗瀏覽記錄，都要重新輸入邀請碼同整過角色。

**會唔會收錢？**
Firebase 嘅免費方案（Spark）每日都有免費用量，一班朋友玩通常夠用。用爆咗只會暫停到第二日，唔會自動收費，除非你自己升級到付費方案。

**改咗 `index.html` 點更新？**
入 GitHub repo，撳返個檔案再撳鉛筆圖示改，或者重新上傳覆蓋。一兩分鐘後網站就會更新。
