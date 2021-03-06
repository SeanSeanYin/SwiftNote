# Basic functions

* **抓取手機資訊**

  * 語言

  ```text
  let langStr = Locale.current.languageCode
  ```

  * 使用者設置的手機名稱

  ```text
  let deviceName = UIDevice.currentDevice().name // 例如： 我的手機
  ```

  * 系統名稱

  ```text
  let sysName = UIDevice.currentDevice().systemName // 例如： iPhone O
  ```

  * 作業系統版本

  ```text
  let sysVersion = UIDevice.currentDevice().systemVersion // 例如：9.2
  ```

  * 裝置唯一識別碼

  ```text
  let uuid = UIDevice.currentDevice().identifierForVendor?.UUIDString  // 例如：FBF2306E-A0D8-4F4B-BDED-9333B627D3E6
  ```

  * 設備型號

  ```text
  let model = UIDevice.currentDevice().model // 例如：iPhone
  ```

* **抓取App資訊**

  ```text
  let infoDic = NSBundle.mainBundle().infoDictionary 
  let appVersion = infoDic?["CFBundleShortVersionString"] // App的版本
  let appBuildVersion = infoDic?["CFBundleVersion"] // App的build版本
  let appName = infoDic?["CFBundleDisplayName"] // App的名稱
  ```

* **獲取UUID**
  * `UIDevice.current.identifierForVendor!.uuidString`
  * 現在的UUID是表示這個Vender在這台裝置上的unique ID，若是移除掉這Vender的所有App後再重新安裝App，UUID會不一樣
* **Guard**

  guard 條件式 else {

  `//當條件式為false要執行的程式`

  `return`

  }

  ```text
    由於`guard`只判斷`true or false`，要注意條件式不能回傳為`optional(true) or optional(false)`
  ```

* **隱藏鍵盤**

  使用[Extension Class](https://github.com/SeanSeanYin/SwiftNote/tree/b2c590e7680ea2ec73716d1670e0f6a11c2b2803/com/questions/24126678/close-ios-keyboard-by-touching-anywhere-using-swift/README.md)的方式來擴充隱藏鍵盤功能，可支援任意個ViewController。

* **獲取時間的用法**
  * 先獲取現在時間

    ```text
    let now = NSDate()
    ```

  * 再轉成unix時間since1970

    ```text
    let timeInterval:TimeInterval = now.timeIntervalSince1970
    ```

  * 再用Int轉成10位數

    ```text
    let timeStamp = Int(timeInterval)
    ```

  * 轉成人類看得懂的格式

    ```text
    let dformatter = DateFormatter()
    dformatter.dateFormat = "yyyy年MM月dd日 HH:mm:ss"
    ```

  * 列印出來結果

    ```text
    print("目前日期時間：\(dformatter.string(from: now as Date))")
    ```

  * DatePicker內的時間想要顯示成24小時制，不要設定`DatePicker的locale`屬性
* **陣列的Search方法**

  ```text
  matchingItems = self.cafes.filter { term in
            return (term.name.contains(searchBarText) || term.address.contains(searchBarText))}
  ```

* **取得時間的年、月、日**

```text
Calendar.current.component(.year, from: date) //年
Calendar.current.component(.month, from: date) //月
```

* **比較某個物件是否為特定class**

```text
obj is UIView
```

* **將圖片轉成NSData**

`UIImagePNGRepresentation(result.forwardImg as! UIImage)! as NSData`

* **NSPredicate要使用Bool的方法**

```text
let predicate = NSPredicate(format: "isFinished == %@", NSNumber(booleanLiteral: false))
```

* **給系統字型的方式**

```text
titleLabel.font = UIFont.boldSystemFont(ofSize: 24 * scale)
titleLabel.font = UIFont.systemFont(ofSize: 24 * scale, weight: UIFontWeightBold)
```

* **selector語法**

  `#selector(ViewController.getData(name:))`

* **讓使用者跳到此App在手機內的設定頁面**
* ```text
  if #available(iOS 10.0, *) {
      UIApplication.shared.open(appSettings, options: [:], completionHandler: nil)
  }else {
      UIApplication.shared.openURL(appSettings)
  }
  ```

  * \*\*\*\*[**各個頁面的URL**](https://stackoverflow.com/questions/28152526/how-do-i-open-phone-settings-when-a-button-is-clicked-ios)\*\*\*\*
* **給UI元件Constrain的方式**

```text
// item:子元件 toItem:父元件
NSLayoutConstraint(item: image, attribute: .topMargin, relatedBy: .equal, toItem: scrollView, attribute: .topMargin, multiplier: 1.0, constant: 20.0 * scale).isActive = true
```

* **轉移到AppStore的評分頁面**

  ```text
  // 唯一需要改的就是 id+AppID (id1190355913)
  let openAppStoreForRating = "itms-apps://itunes.apple.com/gb/app/id1190355913?action=write-review&mt=8"
  if UIApplication.shared.canOpenURL(URL(string: openAppStoreForRating)!) {
     UIApplication.shared.openURL(URL(string: openAppStoreForRating)!)
  }
  ```

* **Textfield的placeholder要變換顏色**
  * 先點選textfield，再選擇IB的Identity inspector
  * 然後在User Defined Runtime Attributes內新增一筆record
  * Key Path的值為：`_placeholderLabel.textColor`，Type選擇Color，Value就選顏色
* **獲得高度**

  * 螢幕高度

  ```text
  UIScreen.main.bounds.size.height
  ```

  * Navigation高度

  ```text
  (self.navigationController?.navigationBar.frame.size.height)!
  ```

  * TabBar高度

  ```text
  (self.tabBarController?.tabBar.frame.height)!)
  ```

