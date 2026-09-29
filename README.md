# PhyloAtlas

PhyloAtlas 是一個原生 macOS 桌面 App，用來把 phylogeny tree 與樣本照片放在同一個畫面中比較。

它不需要 Docker、Python、NAS server 或其他背景服務。Tree、照片與設定都在本機處理，適合需要反覆比較親緣關係與樣本形態的研究工作。

![PhyloAtlas 初始畫面](docs/images/phyloatlas-empty.png)

## 為什麼開發 PhyloAtlas

我主要研究珊瑚（Acropora）族群的遺傳與演化。珊瑚的形態、物種與演化關係常常不容易區分；形態多樣性也使樣本之間的親緣關係、物種分界與形態辨識變得困難。

單獨查看 phylogeny tree 很難同時對照實際形態，逐一在資料夾中尋找照片也不容易維持樣本與 node 的對應。因此我開發 PhyloAtlas，讓 tree 上的 node 可以直接對應到照片資料夾，並在同一個介面中比較親緣關係與形態。

PhyloAtlas 不限於珊瑚。只要有照片、phylogeny tree，以及適當的 node 命名規則，就可以用來整理與比較不同類群或不同研究資料集。

## 主要功能

### Tree 與照片對照

- 讀取 `.tree`、`.treefile`、Newick、`.nex`、`.nexus` 等常見 tree 格式。
- 使用 PearTree 顯示 phylogeny tree，支援縮放、搜尋、篩選、排序、旋轉、clade 操作、定根與顏色／標註等功能。
- 點選單一 node、內部 node 或 clade，即可在右側查看對應照片。
- Tree 與照片面板可以獨立調整寬度，也可以隱藏照片面板以最大化 tree 顯示空間。

![PhyloAtlas Tree 與照片比較](docs/images/phyloatlas-workspace.png)

### Node 與照片資料夾

- 自動讀取 tree 中的 node 名稱。
- 依照 node 命名規則尋找對應的照片資料夾。
- 支援完整名稱、前導欄位與正規表示式等 matching 方式。
- 可使用 delimiter 與指定欄位。例如 `S14_Asolitaryensis_KeelungWaimushan` 使用 `_` 的第一個欄位時，對應資料夾鍵值為 `S14`。
- 可以依照 tree 建立缺少的 node 資料夾。
- 只建立不存在的資料夾，不會覆蓋既有資料夾，也不會刪除舊樣本資料夾。
- 新增照片後可以重新讀取照片資料夾，不需要重新載入 tree。

### 代表照片與 grid

- 每個 node 可以選取一張或多張代表照片。
- 選擇多個 node 或 clade 時，右側只顯示已選取的代表照片。
- 使用每列照片數的滑桿、`−`／`+` 按鈕調整 grid。
- 「最佳化」會依目前照片面板大小與照片數量，選擇適合的照片排列。
- 觸控板 pinch out 會放大照片，pinch in 會顯示更多照片。
- 照片過多時會在照片面板內向下捲動，不會產生多組互相干擾的捲動條。
- 點照片可進入沉浸式檢視，雙擊照片可使用 macOS 預設程式開啟。

### Node 搜尋與更名

- 搜尋 tree 中的 tip label，並以「上一個／下一個」切換結果。
- 可以直接對目前選取的 node 開啟更名面板。
- 支援一般文字、正規表示式與批次搜尋取代。
- 更名前會顯示「更改前 → 更改後」的完整預覽。
- 可同步更改對應的照片資料夾名稱。
- 支援匯入 CSV／TSV，依 identifier 精確批次更新 node 名稱，避免把 `S1` 誤改到 `S11`。
- 寫回 tree 時保留原始 tree 檔案結構，不重新產生整棵 tree。

![PhyloAtlas node 更名](docs/images/phyloatlas-rename.png)

### 匯出

- 使用 PearTree 原生功能匯出 Tree，可選擇 NEXUS 或 Newick 等格式。
- 匯出 PDF，包含目前的 tree 與照片配置。
- 匯出 SVG，讓 tree branch、文字與照片可以在 Illustrator 等影像軟體中繼續編輯。
- 可在匯出 PDF 時指定輸出尺寸。

### 設定與語言

- 支援 English、繁體中文與日本語。
- 可依 macOS 系統語言自動選擇介面語言。
- 可調整 PearTree 工具列，依分類及個別項目顯示或隱藏功能。
- 可調整 tree 顯示方式、節點選取標記樣式、照片 matching、定根／外群與資料夾警告。

![PhyloAtlas 設定面板](docs/images/phyloatlas-settings.png)

## 使用流程

1. 按「載入 Phylogeny Tree」，選擇 tree 檔案。
2. 按右側「照片資料夾」，選擇照片根目錄。
3. 確認「設定 → 照片資料夾」中的 node 與資料夾 matching 規則。
4. 點選 Tree 中的 node 或 clade，查看相對應的照片。
5. 如有缺少的資料夾，可從「設定 → 節點選取」按下建立 tree node 資料夾。
6. 在照片中勾選代表照，再選取其他 node 進行比較。

## 設定面板簡介

| 面板 | 用途 |
| --- | --- |
| 語言 | 選擇系統預設、English、繁體中文或日本語。 |
| 節點選取 | 搜尋 node、選取 node、建立缺少的 node 資料夾，以及調整 selected marker 樣式。 |
| Tree 設定 | 調整原始、比例或等長的 branch display，並儲存 PearTree 顯示設定。 |
| PearTree 工具列 | 分類控制 PearTree 工具列及其個別功能。 |
| 照片資料夾 | 設定 node label 如何轉換成照片資料夾鍵值。 |
| 定根／外群 | 使用原始 root、單一外群、多個外群、MRCA 或 midpoint root。 |
| 匯入 CSV 批次更名 | 依 identifier 精確更新 node 名稱並預覽結果。 |
| Folder warnings | 查看找不到、重複或有多個候選資料夾的 node。 |

![PhyloAtlas 設定面板中的各項功能](docs/images/phyloatlas-settings.png)

## 支援的資料夾規則

假設 node 名稱如下：

```text
S14_Asolitaryensis_KeelungWaimushan
```

使用 delimiter `_` 與前導欄位 `1` 時，PhyloAtlas 會使用第一個欄位 `S14` 作為照片資料夾鍵值。建立資料夾與尋找資料夾會使用同一套規則，避免 node 改名或新增樣本後產生不一致的對應結果。

照片可以放在對應資料夾中，PhyloAtlas 會遞迴讀取支援的影像格式，包括 JPG、JPEG、PNG、GIF、WebP、TIFF 與 BMP。

## macOS 版本

目前版本是原生 macOS standalone App，最低支援 macOS 13。GitHub Releases 會提供 `.dmg` 檔案。

第一次開啟未簽署的 App 時，如果 macOS 阻擋啟動，可以在 Finder 對 App 按住 Control 再選擇「打開」，或依 macOS 顯示的安全性提示允許開啟。

## PearTree 與第三方授權

PhyloAtlas 內嵌 PearTree viewer。第三方授權與著作權資訊隨 App 一起附在 `THIRD-PARTY-NOTICES.md`，重新散布時請一併保留。
