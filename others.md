* #### 在Objective C專案內，使用Swift Class的步驟
  * 先從File -> File，
  * 在剛剛宣告的Class前面新增@objc
  * 在Project和Target的Build Settings內，把下面的值
   * Always Embed Swift Standard Libraries = YES
   * Defines Module = YES
   * Install Objective-C Compatibility = YES
   * Objective-C Generated Interface Header Name = -Swift.h
  * 在想要使用Swift Class的檔案內  #import "projectName-Swift.h"
 * 在Xcode的Product內選擇Clean（Shift + Cmd +K）
 * 重新Run（Cmd + R）

   
