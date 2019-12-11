# Android Franment

## 設計自定義 Fragment

### 繼承 Fragment

``` kotlin
class MyFragment : Fragment()
```

### 覆寫 onCreatedView()

``` kotlin
class MyFragment() : Fragment() {
    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {
        return inflater.inflate(R.layout.my_fragment, container, false)
    }
}
```

inflate() 的第一個參數放 Fragment 的 Layout 檔，第二個參數放傳入的 container。

### 建議設計單一物件化 (singleton)

``` kotlin
class MyFragment() : Fragment() {
    companion object {
        val instance: MyFragment by lazy { MyFragment }
    }

    override fun onCreateView(inflater: LayoutInflater, container: ViewGroup?, savedInstanceState: Bundle?): View? {
        return inflater.inflate(R.layout.my_fragment, container, false)
    }
}
```

<!--success-->
利用 Kotlin 的 by lazy 語法，可輕鬆設計單一物件 (singleton)
<!--success-->

## 在 Activity 中使用 Fragment

### 在 Activity 的 Layout 中放一個容器擺放 Fragment

ConstrainLayout 即可當作容器使用

``` xml
<?xml version="1.0" encoding="utf-8"?>

<androidx.constraintlayout.widget.ConstraintLayout
        xmlns:android="http://schemas.android.com/apk/res/android"
        xmlns:tools="http://schemas.android.com/tools"
        xmlns:app="http://schemas.android.com/apk/res-auto"
        android:layout_width="match_parent"
        android:layout_height="match_parent"
        app:layout_behavior="@string/appbar_scrolling_view_behavior"
        tools:showIn="@layout/app_bar_main"
        tools:context=".MainActivity"
        android:id="@+id/constrain"
/>
```

<!--info-->
若 Layout 中沒有其他 View ，可用最外層的 ConstrainLayout
<!--info-->

### 在 Activity 中放入 Fragment

1. 用 getSupportFragmentManager() 取得 Fragment Manger
2. 用 Fragment Manger 的 beginTransaction() 方法開始 Fragment 的交易
3. 交易完成後記得 Commit()

``` kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        val manager = supportFragmentManager
        val transaction = manager.beginTransaction()
        transaction.replace(R.id.constrain, MainFragment.instance)
        transaction.commit()
    }
}
```

<!--success-->
`transaction.replace() ` 的第一個參數放容器 (Container) ，可用上一步設計 ConstrainLayout 當作容器，第二個參數就是放 Fragment 的實體，因有單一物件設計 (singleton)，故用 instance 取得 Fragment 物件。
<!--success-->