# Android Room

`Android` 的資料庫是使用 `SQLite` 資料庫，但 `SQLite` 在 `Android` 中編寫困難，`Google` 提供了新的類別 `Room` 來大幅度簡化程式碼的複雜度。`Room` 編寫簡化很多，只需要設計資料模型 `Entity`、資料存取物件 `Dao`、資料庫 `Database`，簡化許多代碼，並且易讀許多。

## 導入 Room

```grovy
apply plugin: 'kotlin-kapt'

dependencies {
    def room_version = "2.2.0-alpha01" // 2.1.0 for latest stable version
    implementation "androidx.room:room-runtime:$room_version"
    kapt "androidx.room:room-compiler:$room_version" // For Kotlin use kapt instead of annotationProcessor
    implementation "androidx.lifecycle:lifecycle-viewmodel-ktx:2.0.0"
}
```

最新版本請參考 [Room](https://developer.android.com/jetpack/androidx/releases/room) 官網

## 使用範例

假設我們要儲存使用者的資料，包括使用者的 ID 、名字、性別，三樣資料。

### 設計資料模型 (Entity)

使用 `Kotlin` 的 `Data Class` 設計使用者的資料模型，在類別上方標示為 `Entity`，當中包含三樣資料，並在其中的 `id` 屬性標示為 `PrimaryKey`。

需要確保每個使用者的 ID 都不會重複，PrimaryKey 是識別每個資料不同的方法。

```Kotlin
import androidx.room.Entity
import androidx.room.PrimaryKey

@Entity
data class User(
    @PrimaryKey val id: Int,
    val name: String,
    val sex: Boolean
)
```

### 設計 Dao

Dao 為一個介面 (Interface)，設計 UserDao 介面標示為 Dao，在裡面定義`讀取資料`、`新增資料`、`刪除資料`的方法。

* Query 標記裡放 Query 語法
* Insert 標記裡面放當資料重複時的處理方式，有三種辦法：
  * Replace
  * Abort
  * Ignore

```kotlin
import androidx.room.*

@Dao
interface UserDao{
    @Query("select * from user")
    fun getAllUsers() : List<User>

    @Insert(onConflict = OnConflictStrategy.REPLACE)
    fun addUser(user: User)

    @Delete
    fun deleteUser(user: User)
}
```

### 設計 Database

設計一個抽象類別 (abstract class) 繼承 RoomDatabase，然後標記為 Database。

@Database 標記的參數：

* 要儲存的 Entity 類別
* 檔案版本

```kotlin
import androidx.room.Database
import androidx.room.RoomDatabase

@Database(entities = arrayOf(User::class), version = 1)
abstract class UserDatabase : RoomDatabase() {
    abstract fun getUserDao() : UserDao
}
```

### 在 Activity 中使用

```kotlin
val db = Room.databaseBuilder(this, UserDatabase::class.java, "user-db")
            .allowMainThreadQueries() // 允許在主執行續中執行
            .build();
```

不建議在真正使用時使用主執行續 (Main Thread) 產生 Database 物件，這會耗費很大的系統資源。