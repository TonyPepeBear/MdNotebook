# 在 Mac 上執行 C++ 文件

## 安裝附加功能

在 `vscode` 中安裝 [**Code Runner**](https://github.com/formulahendry/vscode-code-runner) 附加功能。

## Run

用 `⌃⌘N` 快捷鍵執行檔案。

## Run in Terminal

若需要 `input` 資料，那就需要開啟 Run in Terminal 的選項，在設定中的選項打勾即可。

### 副檔名

預設輸出的檔案是沒有副檔名的，若需要用 `git` 管理可能會很不方便，需要修改代 `settings.json` 來增加副檔名。

開啟 `settings.json` 後新增下列代碼：

``` json
{
    "code-runner.executorMap": {
        "cpp": "cd $dir && g++ $fileName -o $fileNameWithoutExt.out && $dir$fileNameWithoutExt.out"
    }
}
```

修改後就用 `out` 當副檔名。

