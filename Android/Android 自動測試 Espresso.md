---
title: Android 自動測試 Espresso
preview: 
date: 2021/05/27
tag: 
  - android
  - espresso
---

Android 的 UI 自動測試

## 導入 Espresso

```gro
android {
    defaultConfig {
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"
    }
}
```

```groovy
dependencies {
    testImplementation 'junit:junit:4.12'
    androidTestImplementation 'androidx.test:runner:1.1.1'
    androidTestImplementation 'androidx.test:rules:1.1.1'
    androidTestImplementation 'androidx.test.ext:junit:1.1.0'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.1.1'
}
```

記得使用最新版本： [Espresso setup instructions](https://developer.android.com/training/testing/espresso/setup)

## 使用範例

```kotlin
import androidx.test.espresso.Espresso.onView
import androidx.test.espresso.action.ViewActions.*
import androidx.test.espresso.assertion.ViewAssertions.matches
import androidx.test.espresso.matcher.ViewMatchers.*
import androidx.test.ext.junit.runners.AndroidJUnit4
import androidx.test.rule.ActivityTestRule
import org.junit.Rule
import org.junit.Test
import org.junit.runner.RunWith

@RunWith(AndroidJUnit4::class)
class MainActivityTest {
    @get:Rule
    val mainActivityRule = ActivityTestRule(MainActivity::class.java)

    @Test
    fun guessFiveTimes() {
        val activity = mainActivityRule.activity //取得 Activity
        onView(withId(R.id.editText)).perform(typeText("message") //在 EditText 中輸入文字
        onView(withId(R.id.button)).perform(click()) //點擊按鈕
        onView(withText(message)).check(matches(isDisplayed())) //確認 message 是否在畫面上
        onView(withText(R.string.play_again)).perform(click()) //用文字尋找 View 並點擊
    }
}
```
