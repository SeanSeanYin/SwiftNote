* #### 加入placeholder的方式

  * 先置入 `UITextViewDelegate`

  * 在 textViewDidBeginEditing 來判斷是否開始編輯

  ```
      func textViewDidBeginEditing(_ textView: UITextView) {
          if textView.text == NSLocalizedString("Review Content", comment: "") {
              textView.text = ""
              textView.textColor = UIColor.black
          }
          textView.becomeFirstResponder()
      }
  ```

  * 在 textViewDidEndEditing 來判斷是否結束編輯

  ```
      func textViewDidEndEditing(_ textView: UITextView) {
          if textView.text == "" {
              textView.text = NSLocalizedString("Review Content", comment: "")
              textView.textColor = UIColor.lightGray
          }
          textView.resignFirstResponder()
      }
  ```

* #### 計算字數

  * 在shouldChangeTextIn內來統計字數

  * ```
        func textView(_ textView: UITextView, shouldChangeTextIn range: NSRange, replacementText text: String) -> Bool {
        
            if(text == "\n") {
                textView.endEditing(true)
                return false
            } else {
            
                let count = (textView.text?.characters.count)! + text.characters.count - range.length
                self.showWords(count: self.maxContentCount - count)
            
                if (self.maxContentCount - count) < 0 {
                    self.postButton?.isEnabled = false
                } else { self.postButton?.isEnabled = true }
            
                return true
            }
        }
    ```



