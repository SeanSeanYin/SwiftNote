* #### 在Objective C專案內，使用Swift Class的步驟
  * 先從File -> File，
  * 在剛剛宣告的Class前面新增@objc
  * 選擇Build Settings，把下面的值
   * Always Embed Swift Standard Libraries = YES
   * Defines Module = YES
   * Install Objective-C Compatibility = YES
   * Objective-C Generated Interface Header Name = -Swift.h

   
