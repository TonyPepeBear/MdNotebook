---
title: Android Anko 函式庫
preview: Anko 是一個 Kotlin 函式庫，讓開發 Android App 時可以更快速和簡單，可以讓程式碼更清楚明瞭 
date: 2021/05/22
tag: 
  - Android Anko 函式庫 
---

Anko 是一個 Kotlin 函式庫，讓開發 Android App 時可以更快速和簡單，可以讓程式碼更清楚明瞭

## 導入 Anko

```gradle
buildscript {
    ext.anko_version = '0.10.8'
}
```

```gradle
dependencies {
    implementation "org.jetbrains.anko:anko:$anko_version"
}
```

最新版本請參考官方 [GitHub](https://github.com/Kotlin/anko)

## Anko Intent

### 利用 intentFor<>() 的語法

```kotlin
startActivity(intentFor<SomeOtherActivity>()
```

### 若要加入 Extra

```kotlin
startActivity<SomeOtherActivity>(
    "id" to 5,
    "city" to "Denpasar"
)
```

### 其他常用 Intent

| Goal            | Solution                        |
| --------------- | ------------------------------- |
| Make a call     | makeCall(number)                |
| Send a text     | sendSMS(number, [text])         |
| Browse the web  | browse(url)                     |
| Share some text | share(text, [subject])          |
| Send an email   | email(email, [subject], [text]) |

## Anko 對話框

### Toast

```kotlin
toast("Hi there!")
toast(R.string.message)
longToast("Wow, such duration")
```

### Alert

```kotlin
alert("Hi, I'm Roy", "Have you tried turning it off and on again?") {
    yesButton { toast("Oh…") }
    noButton {}
}.show()
```

### AsyncTask

```kotlin
doAsync {
    var result = runLongTask()
    uiThread {
        toast(result)
    }
}
```