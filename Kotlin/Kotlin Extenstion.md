---
title: Kotlin Extenstion Function
preview: Kotlin 相比 Java 提供了需多的語言特性，我認為其中最重要的一個，就是提供了 Extension Function，能在不繼承類別的情況下，對類別增加新的方法，讓程式有更多的靈活性。
date: 2021/05/19
tag: 
  - Kotlin
  - Android
--- 

Kotlin 相比 Java 提供了需多的語言特性，我認為其中最重要的一個，就是提供了 Extension Function，能在不繼承類別的情況下，對類別增加新的方法，讓程式有更多的靈活性。


## 先舉例：在 Android 中使用 Log

以往的寫法

```kotlin
class MyActivity: AppCompatActivity(){
    override fun onCreate(savedInstanceState: Bundle?) {
        su
}
```

這樣的寫法需要定義TAG

## 利用 Kotlin Extension

建立一個叫 Extensions.kt 的檔案，並在其中新增下列程式碼，擴充 Activity 類別。

```kotlin
fun Activity.logd(log: String) {
    Log.d(this::class.java.simpleName, log)
}
```

即可在所有 Activity 的子類別中使用 logd 方法，就不用在每個 Activity 中定義 TAG。

```kotlin
class MyActivity: AppCompatActivity(){
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_my)
        logd("onCreated: ")
    }
}
```