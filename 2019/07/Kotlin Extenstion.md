# Kotlin Extenstion

## 在 Android 中使用 Log

### 以往的寫法

``` kotlin
class MyActivity: AppCompatActivity(){
    override fun onCreate(savedInstanceState: Bundle?) {
        su
}
```

這樣的寫法需要定義TAG

## 利用 Kotlin Extension

建立一個叫 Extensions.kt 的檔案，並在其中新增下列程式碼，擴充 Activity 類別。

``` kotlin
fun Activity.logd(log: String) {
    Log.d(this::class.java.simpleName, log)
}
```

即可在所有 Activity 的子類別中使用 logd 方法，就不用在每個 Activity 中定義 TAG。

``` kotlin
class MyActivity: AppCompatActivity(){
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_my)
        logd("onCreated: ")
    }
}
```