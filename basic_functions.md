# Basic functions

* ### 抓取手機目前的語言

  * `let langStr = Locale.current.languageCode`
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
  



