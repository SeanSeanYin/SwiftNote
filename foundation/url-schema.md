# URL Scheme

* **開啟別的App**

  ```text
  let url = URL("otherAppUrlScheme://")
  UIApplication.shared.open(url!)
  ```

* 別App的Scheme要加入白名單，在調用`UIApplication.shared.canOpenURL(url!)`才能檢查成功

  * 但白名單只對canOpenURL有效，即使沒加入白名單，使用open仍然可以直接開啟
  * 在plist-&gt;新增

  ```text
  <key>LSApplicationQueriesSchemes</key> 
      <array>
             <string>weixin</string>
      </array>
  ```

* **被開啟的App**
  * 新增自己的URL Scheme的方式：`Project->Target->Info->URL Type->URL Schemes`
  * 要parse url內的參數的用法

    ```text
    var userInfo:Dictionary<String, String> = Dictionary()
    let components = URLComponents(url: url, resolvingAgainstBaseURL: false)
        if let queryItems = components?.queryItems {
            for item in queryItems {
                userInfo[item.name] = item.value
            }
        }
    ```
* **開啟自己App的設定頁面**

  * 不能用 `prefs:root`，因為是private api，審核會被退件
  * 要用以下方法，會直接帶使用者到此App所有的設定的頁面

  ```text
  if let url = URL(string:UIApplicationOpenSettingsURLString) {
      if UIApplication.shared.canOpenURL(url) {
          UIApplication.shared.open(url, options: [:], completionHandler: nil)
      }
  }
  ```

