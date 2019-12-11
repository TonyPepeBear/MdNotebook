# Kotlin 匿名類別

在 `Android` 開發中會時常使用到匿名類別，`Kotlin` 有簡化編寫匿名類別的語法，到最後甚至只需要一組大括號。

## 一般匿名類別寫法

``` kotlin
button.setOnClickListener(object : View.OnClickListener {
    override fun onClick(view: View?) {
        TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
    }
})
```

用 `object` 關鍵字實作匿名類別

## 在 Kotlin 中，若匿名類別只有一個方法，可簡化成這樣

``` kotlin
button.setOnClickListener({ view ->
    TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
})
```

## 若只有一個參數可省略

``` kotlin
button.setOnClickListener({
    TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
})
```

若要呼叫省略的參數，則用 `it`

## 若匿名類別為方法的最後一個參數可移出括號外

``` kotlin
button.setOnClickListener() {
    TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
}
```

## 若參數只有匿名類別，可省略括號

``` kotlin
button.setOnClickListener{
    TODO("not implemented") //To change body of created functions use File | Settings | File Templates.
}
```

