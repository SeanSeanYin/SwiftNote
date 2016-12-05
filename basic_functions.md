# Basic functions

* 抓取手機目前的語言
  * ```let langStr = Locale.current.languageCode```
* 獲取UUID
  * ```UIDevice.current.identifierForVendor!.uuidString```
  * 現在的UUID是表示這個Vender在這台裝置上的unique ID，若是移除掉這Vender的所有App後再重新安裝App，UUID會不一樣