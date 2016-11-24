
# SHA1
####參考[stack overflow](http://stackoverflow.com/questions/39684092/swift-3-making-sha1-sha256-and-md5-functions)這篇

先在專案新增一個```objective-c```的file，xcode會自動生成```ProjectNname-Bridging-Header.h```，然後可以將剛剛新增的objective.m檔案移除

並且在此.h檔案內新增 `#import <CommonCrypto/CommonHMAC.h>`

然後置入以下的Extension
```
extension Int {

    func hexString() -> String {
    
        return String(format: "%02x", self)
    }
}

extension Data {

    func hexString() -> String {
        let string = self.map{Int($0).hexString()}.joined()
        return string
    }
    
    func sha1() -> Data {
        
        var result = Data(count: Int(CC_SHA1_DIGEST_LENGTH))
        _ = result.withUnsafeMutableBytes {resultPtr in
            self.withUnsafeBytes{(bytes: UnsafePointer<UInt8>) in
            CC_SHA1(bytes, CC_LONG(count), resultPtr)
            }
        }
        return result
    }
}

extension String {

    func hexString() -> String {
        return self.data(using: .utf8)!.hexString()
    }
    
    func sha1() -> String {
        return self.data(using: .utf8)!.sha1().hexString()
    }
}
```

然後在程式內如下調用：
```signature = signature.sha1()```

