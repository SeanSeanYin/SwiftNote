* #### 開啟別的App
   
 ```
 let url = URL("otherAppUrlScheme://")
 UIApplication.shared.open(url!)
 ```
 
* 別App的Scheme要加入白名單，在調用`UIApplication.shared.canOpenURL(url!)
`才能檢查成功
 * 但白名單只對canOpenURL有效，使用open仍然可以直接開啟
 * 在plist->新增
 
 ```
 <key>LSApplicationQueriesSchemes</key> 
      <array>
             <string>weixin</string>
      </array>
```