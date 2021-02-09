# Chocolatey - Windows 的套件管理器

在許多 linux 發行版上都有套件管理，像是 apt。在 Windows 上也有類似的解決方案。

Chocolatey 可以用 `choco install <...>` 的方式安裝軟體，不用到官網去下載，更新或移除軟體也更容易。

## 安裝 Chocolatey

安裝 Chocolatey 很簡單，只需要簡單幾步驟

1. 以系統管理員的身分開啟 `powershell`
2. 先執行 `Get-ExecutionPolicy`，如果顯示 `Restricted`，再執行 `Set-ExecutionPolicy AllSigned`。
3. 複製貼上下方的指令，執行後就完成了

```powershell
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

這樣就大功告成，可以執行 `choco -?` 確定有安裝成功。 

## 用 Cocolatey 安裝軟體

安裝軟體只需要 `choco install <...>` 就可以。像是如果要安裝 vim，就可以輸入 `choco install vim`。

`choco install -y <...>`，`-y` 的參數可以省略掉向使用者確認是否要安裝的過程。

Chocolatey 上提供很多的軟體，Google Chrome、Office、VSCode、git 等都可以安裝，可以到 Chocolatey 的官網上搜尋看看有什麼可以安裝。

[Chocolatey 官網](https://chocolatey.org/packages)

## 使用腳本安裝軟體

其實可以先寫好一個腳本，讓新的電腦，或是公司有大量的電腦需要安裝軟體時，就可以寫一個腳本讓電腦自動執行去安裝軟體，就不需要每一台電腦都手動的安裝軟體省下時間。
