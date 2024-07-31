![FL logo](https://github.com/user-attachments/assets/bba3df08-2aed-4c21-909b-f81f852c2469)

# Farmland Android BikeKit

## eBike 開發套件

### 引入方式

- 【**GitHub**】建立 Personal Access Token

    - 於個人 GitHub `Settings` -> `Developer Settings` -> `Personal access tokens` -> `Tokens (classic)`
    - 新增一個新的 Token
        - 點擊 `Generate new token (classic)` 新增 Token
          
        - 輸入 Note
          
          > 隨意輸入，比如輸入此 Token 為甚麼用途之類的
          
        - 權限設置

          僅需勾選 `read:packages` 即可儲存
          ![截圖 2024-07-31 下午1 12 07](https://github.com/user-attachments/assets/f4c6203a-42e1-4cdf-9717-0b6f472c7dde)

- 【**Android Studio**】建立 keysotre.properties

    - 於專案根目錄新增 **keysotre.properties** 檔案
      
      > 建議將此檔案加入 .gitignore
      
    - 於檔案中加上以下內容（無需將字串加上雙引號）
      
      ```groovy
      gpr.usr={{GitHub User ID}}
      gpr.key={{GitHub Personal Access Token}}
      ```

- 設置欲引入的目的地與 Authentication

    - `setting.gradle` - **Groovy**
      
        ```groovy
        def keystoreProperties = new Properties()
        file("keystore.properties").withInputStream {
            keystoreProperties.load(it)
        }
        
        dependencyResolutionManagement {
            repositories {
              maven {
                  url = uri("https://maven.pkg.github.com/farmlandtech/AndroidBikeKit")
            
                  credentials {
                      username = keystoreProperties["gpr.usr"]
                      password = keystoreProperties["gpr.key"]
                  }
              }
            }
        }
        ```

  - `setting.gradle.kts` - **Kotlin DSL**

    ```kotlin
    // 獲取 keystore.properties
    val keystoreProperties = java.util.Properties()
    keystoreProperties.load(java.io.FileInputStream(File("keystore.properties")))
    
    dependencyResolutionManagement {
        repositories {
            google()
            mavenCentral()
            maven { url = uri("https://jitpack.io") }
            maven {
                url = uri("https://maven.pkg.github.com/farmlandtech/AndroidBikeKitPublic")
                credentials {
                    username = keystoreProperties.getProperty("gpr.usr")
                    password = keystoreProperties.getProperty("gpr.key")
                }
            }
        }
    }
    ```

- 引入 BikeKit
  
    - `build.gradle(:app)` - **Groovy**
    
    ```groovy
    dependencies {
      implementation 'com.github.farmlandtech:android-bikekit-public:{{release_version}}'
    }
    ```
    
    - `build.gradle.kts(:app)` - **Kotlin**
    
    ```kotlin
    dependencies {
      implementation("com.github.farmlandtech:android-bikekit-public:{{release_version}}")
    }
    ```
