* #### 計算字數

  * 在 shouldChangeCharactersIn 內計算

  * ```
    func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String) -> Bool {

        let count = (textField.text?.characters.count)! + string.characters.count - range.length
        self.showWords(count: self.maxTitleCount - count)

        if (self.maxTitleCount - count) < 0 {
            self.postButton?.isEnabled = false
        } else { self.postButton?.isEnabled = true }

        return true
    }
    ```

* #### 讓按下return鍵的時候，取消鍵盤
* ```
  func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        
      if(text == "\n") {
          textView.endEditing(true)
          return false
      }
      return false
  }

  ```



