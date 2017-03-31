# String

* #### [String和NSString的差異](http://www.cnblogs.com/dsxniubility/p/4784124.html?utm_source=tuicool&utm_medium=referral)：

  * String是值類型，NSString是參考類型
  * String可直接用 + 來串接字串， NSString要用`append()`
  * String支援`for...in`瀏覽方法`（String.characters）`，NSString不支援
  * String計算字串長度用`String.characters.count`或`String.lengthOfBytes(using: .utf8)`；NSString用`NSString.length`
  * String用 `==` 比較兩字串是否相等，NSString用 `NSString.isEqual(to: String)`來比較字串，但是參數的字串要是String格式，也可以用`NSString.isEqual(object: Any?)`來比較兩物件是否相等
  * String轉數字用`Int(String)`，NSString用`NSString.intValue`
  * String判斷是否為空用`String.isEmpty`，NSString用`NSString.length == 0`
  * String可以用`String.insert(newElement: Character, at: String.Index)`來在特定字元前插入字元（不行插入字串）
* #### [將NSData轉成String](https://medium.com/@tuzaiz/swift-nsdata-string-323ed8a7e3cc#.ht97pz195)

  * 方法  
    `var string : String = NSString(data: data, encoding: NSUTF8StringEncoding)`

  * 實例  
    `var responseString = NSString(data: data!, encoding: String.Encoding.utf8.rawValue)`
* #### 將Double轉成String的方式

  * `let newStr = String(someDouble)`
* #### 計算Image的size

  ```
  var image = info[UIImagePickerControllerOriginalImage] as! UIImage
  var imgData: NSData = NSData(data: UIImageJPEGRepresentation((image), 1)) 
  var imageSize: Int = imgData.length
  ```
* #### 抓取url的路徑

  ```
  if let path = urls?[indexPath.row] {
    cell.textLabel?.text = path.path
  }
  ```
* #### 找尋字串在另一個字串內的位置

  ```
  // 先找出要搜尋的字串在被搜尋字串內的Range
  let index = directory.absoluteString.range(of: documentURL.path, options: .backwards, range: directory.absoluteString.startIndex..<directory.absoluteString.endIndex, locale: nil)
  // 再用substring從某個index開始往後取剩下的字串
  let subDirectoryName = directory.absoluteString.substring(from: (index?.upperBound)!)
  ```
* #### 把字串內的空白字元移除掉

  ```
  let str = " Swift 3.0 "
  let trimmed = str.trimmingCharacters(in: .whitespacesAndNewlines)
  ```
* #### Decode url格式的字串

```
let title = obj["title"].stringValue.removingPercentEncoding
```

# Array

* #### 陣列使用append\(\)

  假設宣告一陣列 `var directoryList:[URL]!` 直接使用`append()`新增元素會遇到`unwrapped error`，原因是這時候的陣列還是`nil`狀態，所以要先給陣列值，像是 `directoryList = getList()` 或是宣告的時候就指定到空陣列 `var directoryList:[URL]! = []`

# NSURL

* #### 獲取url最後的component

  `let fileName = fileURL.lastPathComponent`

# Dictionary

* #### 宣告

  * `var dic:<String, String> = Dictionary()`
  * `var dic = [String, String]()`
  * `var dic:[String, String] = [:]`
  * `var dic:[String, String] = Dictionary()`
* #### 印在Console上

  * `dump(dictionary)`



