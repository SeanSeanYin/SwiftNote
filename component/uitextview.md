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



