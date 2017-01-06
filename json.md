# SwiftyJSON

SwiftyJSON的[gitHub](https://github.com/SwiftyJSON/SwiftyJSON)

[SwiftyJSON 中文教學](http://www.hangge.com/blog/cache/detail_968.html)

* 使用CocoaPods安裝SwiftyJSON的方法
  * 先透過終端機到Project的根目錄建立Podfile
  * 然後貼上以下代碼，並將MyApp改成專案名稱
    ```
    platform :ios, '10.0'
    use_frameworks!
    target 'MyApp' do
    pod 'SwiftyJSON'
    pod 'Alamofire', '~> 4.0'
    end
    ```
  * 再回到終端機輸入pod install，看到終端機顯示`Pod installation complete`即表示完成

* Way for loop in JSON
  * ```
    for (_, subJson) in json["item"] {
       if let title = subJson["title"].string {
           print(title)
       }
    }
    ```

* 寫自己的[API and JSON manager](https://devdactic.com/parse-json-with-swift/)

* 解決無法建立http連線的方法
  * 到plist先新增 ```App Transport Security Settings```
  * 再剛剛建立完成的```App Transport Security Settings```再新增```Allow Arbitrary Loads```，並將boolen值設定為Yes

