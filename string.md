# String

[String和NSString的差異](http://www.cnblogs.com/dsxniubility/p/4784124.html?utm_source=tuicool&utm_medium=referral)：
* String是值類型，NSString是參考類型
* String可直接用 + 來串接字串， NSString要用append()
* String支援for...in瀏覽方法（String.characters），NSString不支援
* String計算字串長度用String.characters.count或String.lengthOfBytes(using: .utf8)；NSString用.length
* String用 == 比較兩字串是否相等，NSString用 NSString.isEqual(to: String)來比較字串，但是參數的字串要是String格式，也可以用isEqual(object: Any?)來比較兩物件是否相等
* String轉數字用Int(String)，NSString用NSString.intValue
* String判斷是否為空用String.isEmpty，NSString用NSString.length == 0
* String可以用String.insert(newElement: Character, at: String.Index)來在特定字元前插入字元（不行插入字串）

[將NSData轉成String](https://medium.com/@tuzaiz/swift-nsdata-string-323ed8a7e3cc#.ht97pz195)
var string : String = NSString(data: data, encoding: NSUTF8StringEncoding)
var responseString = NSString(data: data!, encoding: String.Encoding.utf8.rawValue)


