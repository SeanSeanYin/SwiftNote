* #### 開啟別的App
   
 ```
 let url = URL("otherAppUrlScheme://")
 UIApplication.shared.open(url!)
 ```
 
* 別App的Scheme要加入白名單，在調用`UIApplication.shared.canOpenURL(url!)
`才能檢查成功
 * 在plist