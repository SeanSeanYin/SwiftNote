# Basic function

* #### 抓取手機資訊

  * 語言

    ```
     let langStr = Locale.current.languageCode
    ```

  * ```Swift
    let deviceName = UIDevice.currentDevice().name
    ```

    ```
    //获取设备名称 例如：梓辰的手机
    let
     sysName = UIDevice.currentDevice().systemName 
    //获取系统名称 例如：iPhone OS
    let
     sysVersion = UIDevice.currentDevice().systemVersion 
    //获取系统版本 例如：9.2
    let
     deviceUUID = UIDevice.currentDevice().identifierForVendor?.UUIDString  
    //获取设备唯一标识符 例如：FBF2306E-A0D8-4F4B-BDED-9333B627D3E6
    let
     deviceModel = UIDevice.currentDevice().model 
    //获取设备的型号 例如：iPhone
    ```
  * 使用者設置的手機名稱

  ```
  let deviceName = UIDevice.currentDevice().name
  ```

  * 
* ### 獲取UUID

  * `UIDevice.current.identifierForVendor!.uuidString`
  * 現在的UUID是表示這個Vender在這台裝置上的unique ID，若是移除掉這Vender的所有App後再重新安裝App，UUID會不一樣
* ### Guard

  guard 條件式 else {

  `//當條件式為false要執行的程式`

  `return`

  }

        由於`guard`只判斷`true or false`，要注意條件式不能回傳為`optional(true) or optional(false)`

* ### 隱藏鍵盤

  使用[Extension Class](/com/questions/24126678/close-ios-keyboard-by-touching-anywhere-using-swift)的方式來擴充隱藏鍵盤功能，可支援任意個ViewController。

* ### 獲取時間的用法

  * 先獲取現在時間

    ```
    let now = NSDate()
    ```

  * 再轉成unix時間since1970

    ```
    let timeInterval:TimeInterval = now.timeIntervalSince1970
    ```

  * 再用Int轉成10位數

    ```
    let timeStamp = Int(timeInterval)
    ```

  * 轉成人類看得懂的格式

    ```
    let dformatter = DateFormatter()
    dformatter.dateFormat = "yyyy年MM月dd日 HH:mm:ss"
    ```

  * 列印出來結果

    ```
    print("目前日期時間：\(dformatter.string(from: now as Date))")
    ```

  * DatePicker內的時間想要顯示成24小時制，不要設定`DatePicker的locale`屬性
* #### 陣列的Search方法

  ```
  matchingItems = self.cafes.filter { term in
            return (term.name.contains(searchBarText) || term.address.contains(searchBarText))}
  ```
* #### selector語法

  `#selector(ViewController.getData(name:))`

* #### 讓使用者跳到此App在手機內的設定頁面

  ```
  if #available(iOS 10.0, *) {                            

  UIApplication.shared.open(appSettings, options: [:], completionHandler: nil)
  }
  ```



