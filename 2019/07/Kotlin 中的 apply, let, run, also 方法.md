# Kotlin 中的 apply, let, run, also 方法

## 方便記憶表格

| 方法名 | 表自身物件 | 回傳值   |
| ------ | ---------- | -------- |
| let    | it         | 最後一行 |
| run    | this       | 最後一行 |
| also   | it         | 自身     |
| apply  | this       | 自身     |



 it, run this, also it, apply this

## 使用範例

### let 方法

可很方便判斷 null 的問題

``` kotlin
nullable?.let{
    //DO SOMETHING
}
```

### apply 方法

可方便用於初始化

``` kotlin
AlertDialog.Builder().apply{
    title = "title"
    message = "message"
    setPositiveButton("OK", null)
    show()
}
```

``` kotlin
button.apply {
    visibility = View.VISIBLE
    text = "message"
    setOnClickListener{
        //onClicked
    }
}
```