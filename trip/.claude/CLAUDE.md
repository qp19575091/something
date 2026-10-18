# trip — 旅遊

旅遊行程規劃。每趟旅程一個資料夾，以地點命名，裡面放一個單檔 `index.html`。

`trip/index.html` 是行程目錄頁（GitHub Pages：https://qp19575091.github.io/something/trip/，網站根目錄的「旅遊」卡片連到這裡），每趟行程一張卡片，點開跳到該行程。根目錄卡片上的行程數量與摘要也要一起更新。

## 行程索引

| 資料夾 | 行程 | 日期 |
| --- | --- | --- |
| `京都/` | 關西 8 天 7 夜（京都・丹後・大阪） | 2026/12/24–12/31 |

## 頁面慣例（以 `京都/index.html` 為準）

- 單一 HTML 檔：CSS、JS 都寫在檔案裡，不拆出去
- 語言 `zh-Hant`，字型 Noto Serif TC（標題）＋ Noto Sans TC（內文），從 Google Fonts 載入
- 顏色用 `:root` 的 CSS 變數（`--accent`、`--warm`、`--tag-*` 等），不要寫死色碼
- 地圖用 Leaflet 1.9.4（cdnjs）
- 版面：頂部 sticky 導覽列 → hero（標題、日期、注意事項）→ 行程總覽卡片 → 每日行程 → 附錄
- 附錄常見項目：住宿建議、票券與交通成本比較、風險清單、預約清單、出發前確認清單、餐廳地圖

## 花費記帳

- 每趟行程資料夾有 `expenses.json`（`members` 成員名單、`me` 使用者本人在名單中的名字（「個人花費」預設選他）、`expenses` 已同步的花費），頁面附錄「花費記帳」讀它顯示總覽、分帳、明細
- 使用者在頁面「記一筆」的資料先存在瀏覽器 localStorage（key：`trip-expenses:<地點>`），標「未同步」；按「匯出未同步」下載 `expenses-<地點>-YYYY-MM-DD.json`
- 使用者說「整理花費」時：
  1. 讀 `~/Downloads/expenses-<地點>-*.json`（可能有多個），依 `id` 合併進 `trip/<地點>/expenses.json`，已存在的 id 不重複加入；匯出檔的 `members` 不是 null 就更新成員名單
  2. 依日期排序、檢查金額與付款人合理，有疑問先問
  3. commit + push，並提醒使用者在頁面按「清除已同步的本機紀錄」
- 單筆格式：`{id, date(YYYY-MM-DD 或 pre), item, category(交通/住宿/餐飲/門票/購物/其他), amount, currency(JPY/TWD/USD/EUR/KRW/HKD/CNY), rate(記帳當下 1 單位 = 多少台幣), payer, split([] = 全員), note}`；沒有 currency 的舊資料視為 `expenses.json` 的 `currency`
- 匯率：頁面從 open.er-api.com 抓即時匯率（以台幣為基準），抓不到時用 `expenses.json` 的 `fallbackRates`；總覽、分帳、個人花費都同時顯示行程幣別與台幣

## 新增行程

1. 建立 `trip/<地點>/index.html`，沿用上面的慣例
2. 在本檔的「行程索引」加一列
3. 建立 `trip/<地點>/expenses.json`，並把 `京都/index.html` 的「花費記帳」區塊（CSS、HTML、JS）複製過去，改掉 localStorage key、日期清單與匯出檔名
4. 在 `trip/index.html` 加一張 `.trip` 卡片（`data-start`／`data-end` 出發與回程日期、封面地名、行程名稱、地區、標籤），連到 `<地點>/`，依出發日期新到舊排列；倒數天數由頁面 JS 自動算
