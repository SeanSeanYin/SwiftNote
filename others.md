* #### 在Objective C專案內，使用Swift Class的步驟
  * 先從Xcode的 `File -> New -> File `新增檔案，到最後會詢問要不要自動新增`ProjectName-Bridging-Header.h`檔案，請選擇 `Yes`
  * 在剛剛新增的Swift檔案內，宣告的Class前面新增@objc
  `@objc class SwiftViewController: UIViewController {`
  * 在Xcode的`Project`和`Target`的`Build Settings`內，把參數設定成下面的值
  ```
   * Always Embed Swift Standard Libraries = YES
   * Defines Module = YES
   * Install Objective-C Compatibility = YES
   * Objective-C Generated Interface Header Name = -Swift.h
  ```
  * 在想要使用Swift Class的檔案內  `#import "projectName-Swift.h"`
 * 在Xcode的 Product 內選擇 `Clean（Shift + Cmd +K）`
 * 重新 `Run（Cmd + R）`

   
