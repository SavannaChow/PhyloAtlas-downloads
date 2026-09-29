# PhyloAtlas

PhyloAtlas 是一個原生 macOS App，用來在同一個畫面中比較 phylogeny tree 與樣本照片。

它最初是為了珊瑚（Acropora）族群的遺傳與演化研究而開發。珊瑚的形態多樣性很高，物種分界、形態辨識與親緣關係常常需要同時對照，單獨查看 tree 或逐一開啟照片資料夾都不容易。PhyloAtlas 讓 tree node 可以直接對應樣本照片，方便比較親緣關係與形態差異。

PhyloAtlas 不限於珊瑚。只要有照片、phylogeny tree，以及適當的 node 命名規則，就可以用於其他生物類群與研究資料集。

## 下載

請到 [Releases](https://github.com/SavannaChow/PhyloAtlas-downloads/releases/latest) 下載最新的 `.dmg`。

這個 repository 只提供編譯好的 macOS App，不公開 PhyloAtlas 的原始碼。

## 主要功能

- 讀取 `.tree`、`.treefile`、Newick、`.nex`、`.nexus` 等 tree 格式。
- 在左側顯示 phylogeny tree，右側顯示對應的樣本照片。
- 依 node 命名規則自動尋找或建立照片資料夾。
- 支援完整名稱、前導欄位、delimiter 與指定欄位的資料夾 matching。
- 每個 node 可選擇一張或多張代表照片。
- 選取多個 node 或 clade 時，以 grid 比較代表照片。
- 搜尋 tree node，並支援批次更名與 CSV／TSV 精確批次更名。
- 匯出 Tree、PDF 與可編輯 SVG。
- 支援 English、繁體中文與日本語。

## 安裝

1. 開啟下載的 `.dmg`。
2. 將 `PhyloAtlas.app` 拖曳到右側的 `Applications` 資料夾捷徑。
3. 雙擊 DMG 第二區的 `Copy xattr command.pdf`。
4. 用滑鼠選取指令並按 `⌘C` 複製。
5. 雙擊 `Open Terminal.app`，貼上指令並按下 Enter。
6. 從 Applications 開啟 PhyloAtlas。

## 如果 macOS 阻擋啟動

目前版本尚未使用 Apple Developer ID 簽署與 notarization。請先將 App 拖到 Applications，再開啟 DMG 裡的 `Copy xattr command.pdf`，選取並複製指令，然後開啟 `Open Terminal.app` 貼上：

```bash
xattr -dr com.apple.quarantine "/Applications/PhyloAtlas.app"
```

完成後再從 Applications 開啟 PhyloAtlas。

## 第三方授權

PhyloAtlas 內嵌 PearTree viewer 與其他開源元件。第三方著作權與授權資訊會附在 DMG 內的 `THIRD-PARTY-NOTICES.md`。
