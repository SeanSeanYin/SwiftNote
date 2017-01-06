* #### 在Objective C專案內，使用Swift Class的步驟
  * 先從Xcode的 File -> New -> File新增檔案，到最後會詢問要不要自動新增Bridging-Header.h檔案，請選擇Yes
  * 在剛剛新增的Swift檔案內，宣告的Class前面新增@objc
  `@objc class SwiftViewController `
  * 在Project和Target的Build Settings內，把下面的值
   * Always Embed Swift Standard Libraries = YES
   * Defines Module = YES
   * Install Objective-C Compatibility = YES
   * Objective-C Generated Interface Header Name = -Swift.h
  * 在想要使用Swift Class的檔案內  #import "projectName-Swift.h"
 * 在Xcode的Product內選擇Clean（Shift + Cmd +K）
 * 重新Run（Cmd + R）

   
