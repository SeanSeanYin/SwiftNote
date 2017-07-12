* #### Cell要顯示圓角

  * 先新增一個view（cornerView）在Content View內，並設置寬高和Content View的條件

  * 然後設定 cornerRadius 和 masksToBounds

  ```
  cornerView.layer.cornerRadius = 5
  cornerView.layer.masksToBounds = true
  ```

* #### 圓角在前面幾個Init的cell內，顯示失敗的原因

  * 不要固定xib的cell的高度....

  * 圓角的cornerRadius使用 frame.height / 2，不要使用 frame.width / 2 \(前提是UIImageView的高度跟SuperView有比例關係，因為前幾個Init的cell的frame在width是錯誤的，height是正確的\)



