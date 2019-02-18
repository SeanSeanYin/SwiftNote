# Button

* **讓Button的Title有底線**
* ```text
  var attrs = [NSUnderlineStyleAttributeName : 1] as [String : Any]
  let titleString = NSMutableAttributedString(string:NSLocalizedString("signUpWithEmail", comment: ""), attributes:attrs)
  self.signUpWithEmailButton.setAttributedTitle(titleString, for: .normal)
  ```

