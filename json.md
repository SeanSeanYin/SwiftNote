# JSON 

SwiftyJSON的[gitHub](https://github.com/SwiftyJSON/SwiftyJSON)

[SwiftyJSON 中文教學](http://www.hangge.com/blog/cache/detail_968.html)

* 使用CocoaPods的方法
  * 先透過終端機到Project的根目錄建立Podfile
  * 然後貼上以下代碼，並將MyApp改成專案名稱
```platform :ios, '10.0'
use_frameworks!
target 'MyApp' do
    pod 'SwiftyJSON'
    pod 'Alamofire', '~> 4.0'
end
```
  * 再回到終端機輸入pod install，看到終端機顯示completed即表示完成

