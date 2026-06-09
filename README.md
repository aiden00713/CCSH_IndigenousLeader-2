# 教育部高級中等學校原住民學生青年領袖培育營

這個專案是「教育部高級中等學校原住民學生青年領袖培育營｜南區初階」活動網站，部署在 GitHub Pages。前台主要由 `index.html` 提供單頁式內容瀏覽，資料來源則透過 Google Apps Script API 由 CMS 後台管理。

## 專案架構

```text
.
├── archive/          # 舊版頁面與封存檔案
├── css/              # Bootstrap 與網站樣式
├── document/         # 活動文件、PDF、附件
├── fonts/            # Font Awesome 字型
├── images/           # 網站圖片與 Logo
├── js/               # jQuery、Bootstrap、客製 JS
├── CNAME             # GitHub Pages 自訂網域設定
├── LICENSE           # MIT License
├── README.md         # 專案說明
├── index.html        # GitHub Pages 前台主頁
└── info.html         # 活動系統入口
```

## 前台頁面

`index.html` 採用 hash routing，將多個內容頁整合在同一個頁面中：

- `#home`：首頁
- `#about`：實施計畫
- `#class`：活動課程
- `#news`：錄取學員
- `#notice`：行前通知
- `#reform`：推薦表上傳

導覽列由 API 回傳的頁面名稱更新，並保留 `info.html` 作為「活動系統」入口。

## CMS 與 API

前台透過 Google Apps Script Web App 取得最新資料：

```js
window.CCSH_API = {
  url: 'https://script.google.com/macros/s/AKfycbwv-pxqk1VQ-i3XZpFMWaLhLOu6ToQTXVIdVPWpbRQpt2Y7ENU76zbukwPMHsySrsFX/exec',
  action: 'getPublicData'
};
```

CMS 後台可管理：

- 首頁內容與首頁按鈕連結
- 實施計畫
- 活動課程
- 錄取學員 PDF
- 行前通知
- 推薦表上傳
- LINE@ 官方帳號 ID
- 網站聯絡資訊與部分媒體設定

首頁主標題「教育部高級中等學校<br>原住民學生青年領袖培育營」是前台固定樣式，不會被 API 內容覆蓋。

## 內容顯示規則

- CMS 內容欄位使用 Quill 編輯器產生 HTML。
- 前台會直接渲染 CMS 回傳的 `content_html`。
- 首頁最多顯示 2 個主要按鈕，由 CMS 設定顯示項目與連結。
- PDF 直接以 iframe 嵌入原始 PDF URL，並提供「另開 PDF」按鈕。
- 外部 PDF 來源若禁止 iframe 顯示，使用者仍可透過「另開 PDF」開啟檔案。
- 頁尾包含活動地點、聯絡方式、Facebook 粉絲專頁與 LINE@ 官方帳號，已調整為 RWD 顯示。

## 本機預覽

可用簡易靜態伺服器預覽：

```powershell
python -m http.server 8000
```

開啟：

```text
http://localhost:8000
```

因為正式資料來自 Apps Script API，本機預覽時仍需網路連線才能載入 CMS 資料。

## 部署

網站由 GitHub Pages 部署，主要分支為 `main`。推送到 GitHub 後，GitHub Pages 會自動更新。

自訂網域設定在：

```text
CNAME
```

目前網域：

```text
wilc.work
```

## 維護備註

- 修改前台顯示邏輯時，主要編輯 `index.html`。
- 修改 CMS 後台時，需到 `silc_api` Apps Script 專案更新並使用 `clasp push` 推送。
- 舊頁面已移至 `archive/`，目前前台以 `index.html` 和 `info.html` 為主。
- 若更換 PDF 來源，建議使用可公開存取且允許瀏覽器開啟的網址。

## License

MIT License。詳見 `LICENSE`。
