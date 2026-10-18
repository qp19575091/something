# something

個人雜物收納庫，放各種面向的東西，每個類別一個資料夾。

網站目錄（GitHub Pages）：https://qp19575091.github.io/something/

## 類別

| 資料夾 | 類別 |
| --- | --- |
| `trip/` | 旅遊 |

## 結構慣例

每個類別資料夾各自有 `.claude/`，放該類別的說明與規則；細節看各資料夾，不寫在這份 README。

- 根目錄 `index.html` 是網站目錄「雜物收納櫃」，每個類別一個 `drawer` 卡片（類別色用 `:root` 的 `--cat-<類別>` 變數），連到該類別資料夾
- 每個類別資料夾有自己的 `index.html`，列出該類別底下的項目
- 新增類別時：建立資料夾、在上面的「類別」表加一列、在根目錄 `index.html` 加一張卡片

```
something/
├── README.md        # 專案簡介（本檔）
├── index.html       # 網站目錄（各類別入口）
└── trip/            # 旅遊
    ├── .claude/     # 旅遊類別的說明與規則
    ├── index.html   # 旅遊行程目錄
    └── ...
```
