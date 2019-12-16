# 利用 Screen 在 Linux 中開啟多個 Shell

終端機大多同時只能同時進行一個 `Shell` ，用 `Screen` 指令就可以，可暫時將執行到一半的 `Shell` 卸離 `detach` ，並在需要時再重新連接 `attach` ，來達成多個 `Shell` 的切換，或是背景處理。

## 安裝 Screen

大多數的 Linux 都已經內建了 `screen` 指令，若沒有安裝，可透過套件管理自行安裝

``` bash
sudo apt-get install screen
yum install screen
```

## 使用 Screen

使用 Screen 時，直接在終端機執行即可。

``` bash
screen
```

輸入 `screen` 後會出現一些訊息，按下 `enter` 後就可以進入新的 Shell。

這個新的 Shell 其實跟一般 Shell 沒什麼不同，用的指令在這也都能用。

## 離開 Screen

### 結束 Shell

若要直接結束掉，直接輸入 `exit` 即可離開。

### 暫時 卸離 `Detach`

卸離 `Detach` 可以讓執行到一半的工作在背景繼續執行，不會因為暫時離開就中斷工作。如果需要執行較長時間的工作，例如下載或是上傳，就可以用這 `screen` 來讓工作在背景執行。

若要卸離 `Detach`，先按下 `CTRl+A` 再按下 `d`，就可以卸離目前的 Screen。

需要再重新接回時，利用 `-r` 參數就可以快速的接回上一個卸離的 Screen。

``` bash
screen -r
```

## 同時多個 Screen

若同時執行的多個 Screen 在背景，可以用 `-ls` 參數，顯示出目前執行中的 Screnn。

``` bash
screen -ls
```

要連回指定的 Screen 時，就在 `-r` 參數後加上 Screen 的名字即可，但因為通常名字會很長，所以只需要輸入前幾個字，足以判斷即可。下面的範例兩者都會連回 `9608.pts-0.ubuntu` 這個 Screen。

``` bash
screen -r 9608.pts-0.ubuntu
screen -r 9608
```
## Refrence

- [使用 Screen 指令操控 UNIX/Linux 終端機的教學與範例](https://blog.gtwang.org/linux/screen-command-examples-to-manage-linux-terminals/)
