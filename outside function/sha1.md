
# SHA1
####參考[stack overflow](http://stackoverflow.com/questions/39684092/swift-3-making-sha1-sha256-and-md5-functions)這篇

先在專案新增一個```objective-c```的file，xcode會自動生成```ProjectNname-Bridging-Header.h```，然後可以將剛剛新增的objective.m檔案移除

並且在此.h檔案內新增 `#import <CommonCrypto/CommonHMAC.h>`

然後置入以下的Extension
```
extension String {
    func sha1() -> String {
        let data = self.data(using: String.Encoding.utf8)!
        var digest = [UInt8](repeating: 0, count:Int(CC_SHA1_DIGEST_LENGTH))
        data.withUnsafeBytes {
            _ = CC_SHA1($0, CC_LONG(data.count), &digest)
        }
        let hexBytes = digest.map { String(format: "%02hhx", $0) }
        return hexBytes.joined()
    }
}
```

然後在程式內如下調用：
```signature = signature.sha1()```

