# AndroidBikeKitPublic

> FL-Android 平台 Bike 開發套件

> Core SDK、Bluetooth

## 引入方式

- ### 建立 keysotre.properties

    - 於專案根目錄建立 **keysotre.properties**
    - 將此檔案加入 .gitignore
    - 加上以下內容（不用 " " ）
  ```groovy
  gpr.usr={{GitHub User ID}}
  gpr.key={{GitHub Personal Access Token}}
  ```

- ### setting.gradle

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

- ### build.gradle(:app)

  ```groovy
  dependencies {
      implementation com.github.farmlandtech:androidbikekit:{{release_version}}
  }
  ```
