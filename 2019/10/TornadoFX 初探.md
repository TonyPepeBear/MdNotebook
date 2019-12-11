# TornadoFX 初探

## 簡介

TornadoFX 是專為 Kotlin 開發的 UI Framework

## 導入 Gradle

``` gradle
dependencies {
    implementation 'no.tornado:tornadofx:x.y.z'
}
```

最新版本參考 [官方發布頁面](https://github.com/edvin/tornadofx/releases)

## App 和 基本 View

TornadoFX 的最基本是個 `App` ，這點蠻類似 Android 的開發  

設計一個自己的 `App` 繼承 TornadoFX 的 App ，並在建構子內放入一個自己的 `View` 的 `class`

``` kotlin
import tornadofx.*

class MyApp : App(MyView::class)
```

因為我們還沒寫 `View` 所以這裡會報錯，接下來我們就來設計自己的 `View`  

設計一個自己的 `View` 並繼承 `View` 類別，然後複寫抽象屬性 `root`

``` kotlin
import tornadofx.*

class MyApp : App(MyView::class)

class MyView : View() {
    override val root = vbox {

    }
}
```

但是因為 `vBox` 中沒有任何的東西，所以什麼都不會顯示，那就讓我們在其中加入一個 `button` 和一個 `lable`

``` kotlin
import tornadofx.*

class MyApp : App(MyView::class)

class MyView : View() {
    override val root = vbox {
        button(text = "Press me!")
        label(text = "label")
    }
}
```

`vBox` 會將放入的東西垂直的堆疊起來

注意要 import TornadoFX 的類別，如果 import 錯誤是無法執行的

`borderpane` 提供五種位置對齊，詳細可以參考這篇[文章](https://www.yiibai.com/javafx/javafx_borderpane.html)

1. top
2. bottom
3. right
4. left
5. center

``` kotlin
class MyView : View() {
    val topView = find(TopView::class)
    val bottomView : BottomView by inject()

    override val root = borderpane{
        top<TopView>()
        bottom<BottomView>()
    }
}

class TopView : View() {
    override val root = label("Top View")
}

class BottomView : View() {
    override val root = label("Bottom View")
}
```

更多 `TornadoFX` 的佈局指南可以參考這篇[文章](https://www.jianshu.com/p/e387c5ff38e3)

## 執行 TornadoFX

在 main 方法中用 launch 方法執行自己的 App

``` kotlin
fun main() {
    launch<MyApp>()
}
```

![vBox.png](https://i.loli.net/2019/10/30/Tn5MVsm61fkBp3S.png)

## 用 find() 和 inject() 嵌入

`inject()`方法會 lazily 的分派到屬性中，當屬性第一次被呼叫到時才會產生。`find()`的用法不多，但是 `inject()` 比較常用。

``` kotlin
class MyView : View() {
    val topView = find(TopView::class)
    val bottomView : BottomView by inject()

    override val root = borderpane {
        top = topView.root
        bottom = bottomView.root
    }
}

class TopView : View() {
    override val root = label("Top View")
}

class BottomView : View() {
    override val root = label("Bottom View")
}
```

## Controllers

通常會將 UI 設計分為三個部分：

1. Model: 撰寫商業邏輯和資料存儲
2. View: 顯示資料輸入和輸出
3. Controllers: View 和 Model 的中間層，負責通知彼此

雖然你可以將商業邏輯全部放在 `View` ，但是將他們分開寫可以比較清楚。  

下面的範例，創建的一個簡單的輸入方塊 `TextField` ，他的 `value` 綁定在一個 `observable string property` ，然後當 `Button` 被點擊，就將值寫入資料庫，但我們沒寫資料庫，所以就將他 print 出來就好

``` kotlin
class MyView : View() {
    val input = SimpleStringProperty()
    val controller = MyController()

    override val root = form {
        fieldset {
            field("Input") {
                textfield(input)
            }
            button("Commit") {
                action {
                    controller.writeToDatabase(input.value)
                    input.value = ""
                }
            }
        }
    }
}

class MyController : Controller() {
    fun writeToDatabase(inputValue: String) {
        print("Write $inputValue to database!")
    }
}
```

下面是一個顯示清單的範例

``` kotlin
class MyView : View() {
    val input = SimpleStringProperty()
    val controller = MyController()

    override val root = vbox {
        label("My Fruits")
        listview(controller.fruits)
    }
}

class MyController : Controller() {
    val fruits =
        FXCollections.observableArrayList("Apple", "Banana", "Guava", "Orange")
}
```

我們在一個 `vbox` 中放入了 `label` 和 `listview` ，然後將 `listview` 的 item 設定成 conroller 的的屬性

## 耗時工作

當你呼叫一個 controller 的方法，你必須決定他會立即回傳或是完成耗時工作後更新 UI。TornadoFX提供了一個耗時工作的處理方法 `runAsync`。  
在 `runAsync` 中的程式碼會在背景執行，當需要更新 UI 時，呼叫 `ui` 區塊。

``` kotlin
class MyView : View() {
    val myController = MyController()

    override val root = vbox {
        val textField = textfield()
        button("Update Text") {
            action {
                runAsync {
                    myController.loadText()
                } ui { it ->
                    textField.text = it
                }
            }
        }
    }
}

class MyController : Controller() {
    fun loadText(): String {
        Thread.sleep(1000L) // 模擬耗時一秒
        return "long time text"
    }
}
```

當按下了按鈕，會在背景執行 `loadText()` 的耗時工作，當 `runAsync` 執行完成後，會將回傳值傳到 `ui` 區塊裡，並且更新 `TextField`。

## 參考資料

* [TornadoFX Guide](https://edvin.gitbooks.io/tornadofx-guide/)