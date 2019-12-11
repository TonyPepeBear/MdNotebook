# Swift 基礎語法

## 常數、變數

用 `let` 宣告常數，用 `var` 宣告變數

``` swift
let y = 10
var x = 10
var sum = x + y
```

## 型態推論

上方的變數都被自動推斷成整數型態 `Int` ，以下寫法跟上方結果完全相同。

``` swift
let y: Int = 10
var x: Int = 10
var sum: Int = x + y
```

冒號後方的定義型態基本上是可以省略的，Swift 會自動幫你判斷型態。

## 字串處理

一段文字用雙引號刮起來，並可放入變數中做存取，型態為 `String`

``` swift
var s1 = "This is a string"
var s2: String = "This is a string"
```

s1 和 s2 的結果是一樣的

### 字串相加

用加號連接兩個字串即可相加

``` swift
var h = "Hello"
var name = "Tony"
var message = h + ", I am" + name
```

最後 message 的值是 "Hello, I am Tony"

### 更好的連接方式

``` swift
var h = "Hello"
var name = "Tony"
var message = "\(h), I am \(name)"
```

message 的結果一樣是 "Hello, I am Tony"

在雙引號內用反斜線加括號 "\\(變數)" 可以直接帶入變數

### 大小寫轉換

`String` 有內建的方法可以轉換大小寫

``` swift
var name = "Tony"
name.toLowerCase() // tony
name.toUpperCase() // TONY
```

### 字串大小

``` swift
var name = "Tony"
var l: Int = name.count // l = 4
```

## 流程控制

### if、else

與其他程式語言類似，用 `if`、`else` 來處理邏輯判斷

``` swift
var time = 0

if time == 0 {
    print("Time = 0")
} else {
    print("Time != 0")
}
```

`else if` 用於多重邏輯判斷

``` swift
var grade = 60

if grade > 90 {
    print("A")
} else if grade > 80 {
    print("B")
} else if grade > 70 {
    print("C")
} else if grade > 60 {
    print("D")
} else {
    print("F")
}
```

### switch

`switch` 用於多條件判斷

`switch` 一定要有 `default` 才可以執行

``` swift
var season = 3

switch (season) {
case 1:
    print("spring")
case 2:
    print("summer")
case 3:
    print("fall")
case 4:
    print("winter")
default:
    print("not in range")
}
```

區間判斷

``` swift
switch month {
case 1...3:
    print("spring")
case 4...6:
    print("summer")
case 7...9:
    print("fall")
case 10...12 
    print("winter")
default:
    print("not in range")
}
```

