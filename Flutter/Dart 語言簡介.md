# Dart 語言簡介

`Dart` 語言是由 `Google` 開發程式語言，語法簡單，類似 `javascript` ，是物件導向語言，最常見用於 `flutter` 開發跨平台的應用程式。

## 變數

用 `var` 宣告一個可變的變數：

```dart
var name = 'Tony';
var age = 10;
```

不可變動的值有兩種，`final` 的值只能設定一次，`const` 的值是編譯時常數：

```dart
final name = "Tony";
const pi = 3.14;

// 以下嘗試更改會發生錯誤
name = "Pepe";
pi = 0;
```

## 基本資料型態

`Dart` 中的基本資料型態有：`Number`、`String`、`Boolean`、`List`、`Map`。

### Number

Number 包括兩個類：`int`、`double`

* int：整數，值的範圍 `-2^53` ~ `2^53`
* double：浮點數，64位元。

```dart
var age = 10; //int
var weight = 51.2; //double
```

`int` 和 `double` 都是 `num` 的子類：

```dart
num weight = 50;
weight = 51.2;
```

### String

用 `String` 類別儲存字串：

```dart
var name = "Tont";
var name1 = "Pepe";
```

#### String 可用 + 相連

```Dart
var name = "Tont"; + "Pepe";
```

在雙引號中引用：

```dart
var name = "Tont";
print("Your name is $name")
```

### Boolean

只能儲存 `true` 或 `false`

```dart
var sex = true;
```

### List

可存放一系列相同類型的的數據

```dart
var list = [1, 2, 3];
```