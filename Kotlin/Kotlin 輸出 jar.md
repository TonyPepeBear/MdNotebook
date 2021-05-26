# Kotlin 輸出 jar

## 新增 Artifacts

1. 打開 Intellij 的 `Project Structure`
2. 點擊 `Artifacts`
3. 新增 Jar -> From Models with dependencies
4. Model 選 .main
5. MainClass 選有 main function 的 kotlin 檔案，檔案名稱會多上 kt
6. 選 `cope to the output dictionary and link via manifest`
7. Dictionary for META-INF/MANIFEST.MF: 把 `../src/main/kotlin` 換成 `../src/msin/resource`