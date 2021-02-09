# 使用 Rclone 同步資料到雲端硬碟

Rclone 是一個雲端硬碟工具，使用簡單的幾行指令就可以備份、同步電腦的資料到雲端硬碟中，還可以在兩個雲端硬碟中複製或移動檔案。

## 安裝 Rclone

### Linux/macOS

運行下面的指令

```bash
curl https://rclone.org/install.sh | sudo bash
```

### Windows

在[這個](https://rclone.org/downloads/)網頁下載

## Rclone 新增雲端硬碟

運行下面指令進入設定

```bash
rclone config
```

輸入 `n` 新增雲端硬碟，第一個問題是要新增的雲端硬碟的名字，隨便打就可以。然後就根據提示新增就可以。

## 常用指令

### rclone copy

從 source 複製資料到 dest，會自動略過已經存在，或未變更的檔案的檔案，也不會刪除任何的檔案。

如果目標路徑不存在，會自動創建路徑。

```bash
rclone copy source:path dest:path [flags]
```

比較需要注意的是，這個指令只會複製 source 資料夾的內容，並不會複製 source 資料夾。

用 `-P` 參數可以看到傳送中的即時狀態。

### rclone sync

將 source 的資料同步到 dest，會刪除或覆蓋 dest 的內容，但定不會更動 source 的資料，也自動略過已經存在且沒有變更的檔案。

如果目標路徑不存在，會自動創建路徑。

```bash
rclone sync source:path dest:path [flags]
```

<!--warning-->

因為會刪除資料，建議在每次同步前，都先加上 `--dry-run` 或 `-n` 參數，確認哪些檔案會被變更，再同步資料。

用 `-P` 參數可以看到傳送中的即時狀態。

## Refrence

* [Rclone官網](https://rclone.org/)
