* #### 開啟別的App
   
 ```
 let url = URL("otherAppUrlScheme://")
 UIApplication.shared.open(url!)
 ```
 
* 別App的Scheme要加入白名單，在調用`UIApplication.shared.canOpenURL(url!)
`才能檢查成功
 * 但白名單只對canOpenURL有效，即使沒加入白名單，使用open仍然可以直接開啟
 * 在plist->新增
 
 ```
 <key>LSApplicationQueriesSchemes</key> 
      <array>
             <string>weixin</string>
      </array>
```

* #### 被開啟的App
 * 新增自己的URL Scheme的方式：`Project->Target->Info->URL Type->URL Schemes`
 * 要parse url內的參數的用法
```
 var userInfo:Dictionary<String, String> = Dictionary()
 let components = URLComponents(url: url, resolvingAgainstBaseURL: false)
        if let queryItems = components?.queryItems {
            for item in queryItems {
                userInfo[item.name] = item.value
            }
        }
```