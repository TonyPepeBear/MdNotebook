# 在 Gradle 打包 Java、Kotlin 執行檔

打包 Java, Kotin 有許多方法，本篇會介紹一個最簡單的方法，雖然不是最好的方法，但易於各個平台上使用。

## Application

Gradle 有個 [Application](https://docs.gradle.org/current/userguide/application_plugin.html) 的 Plugin，可以快速的產生執行檔，也會自動加入所需依賴，可執行於有安裝 JVM 的 Windows, macOS, Linux。

在 `build.gradle` 中加入 Plugin：

```groovy
plugins {
    id 'application'
}
```

這樣就完成一半了，剩下的唯一一步驟，就是加入 `Main Class` 的定義：

```groovy
application {
    mainClassName = 'org.gradle.sample.Main'
}
```

因為 Kotlin 的 Main Function 是 Top Level，所以 Main Function 不會像 Java 是在一個 Class 裡面，為了在 Jvm 上執行， Kotlin 會自動產生一個 Kotlin File 的檔名加上 Kt 的類別，並且把 Main Function 放在裡面。例如有一個 `Hello.kt` 的 Kotllin 檔案，裡面的 Main Function 就會在 `HelloKt` 這個類別。

## 打包執行檔

設定完成後，只需一句 Gradle 指令，就可以將可執行檔包在 Zip 裡：

```shell
gradle distZip
```

如果要用 Tar 打包：

```shell
gradle distTar
```

如果是用 Gradle Wrapper  的人，就要用 `gradlew`：

```shell
./gradlew distZip
```

## 執行打包後的執行檔

執行完打包指令後，會在專案目錄底下的 `build/distributions` 產生壓縮檔，解壓縮後會有兩個目錄 `bin` 和 `lib`，`lib` 目錄裡都是放專案所有會用到的依賴，基本上不用動他們。要執行檔案，到 `bin` 目錄裡會發現兩的檔案，兩個檔名應該一樣，只是其中一個會有附檔名 `.bat`，有 `.bat`附檔名的就是給 Windows 執行用的，沒有附檔名的就是給 Unix 執行的，`linux` 和 `macOS` 執行的：

```shell
./Hello 
./Hello.bat
```

這樣基本上就大功告成，雖然不適合給一般的使用者使用，但是也是一個最陽春的打包方案，可以應付一些簡單的需求。

## Reference

[The Application Plugin](https://docs.gradle.org/current/userguide/application_plugin.html)
