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

  * 在 cellForRowAt 內，重新計算Cell的Size即可

  ```
  cell.size = CGSize(width: UIScreen.main.bounds.width, height: 190 * self.getScreenScale(with: .height))
  ```
* 更新Cell和Cell內元件的Frame

  * 在要更新的地方呼叫 reloadRow  
    `self.storeTableView.reloadRows(at: [IndexPath.init(row:2, section:0)], with: .automatic)`

  * 然後在 cellForRowAt 內更新Frame，並且在heightForRowAt內傳回Cell的高度

```
func tableView (_tableView:UITableView, cellForRowAt indexPath:IndexPath) ->UITableViewCell {

    switch indexPath.row {
        case2:

        if let descriptionCell = tableView.dequeueReusableCell(withIdentifier:"StoreDescriptionCell")as?StoreDescriptionCell {
           // 計算寬高
           let height = store.storeObj.about!.height(withConstrainedWidth: UIScreen.main.bounds.width *0.9, font: descriptionCell.contentLabel.font)
           let width = store.storeObj.about!.width(withConstraintedHeight: descriptionCell.contentLabel.font.lineHeight, font: descriptionCell.contentLabel.font)

           if height < (descriptionCell.contentLabel.font.lineHeight * 3) {
               descriptionCell.expandableLabel.isHidden =true
           } else { descriptionCell.expandableLabel.isHidden = false }

           if self.isExpand == true{

               descriptionCell.expandableLabel.isEnabled =false
               descriptionCell.expandableLabel.text =""
               descriptionCell.contentLabel.numberOfLines =0
               descriptionCell.contentLabel.sizeToFit()
               self.newContentLabelHeight = height + CGFloat(50) + descriptionCell.descriptionLabel.frame.height
               // 給新的寬高
               descriptionCell.contentView.frame = CGRect(x:0.0, y:0.0, width: UIScreen.main.bounds.width *0.9, height:self.newContentLabelHeight)
               self.storeTableView.layoutIfNeeded()
            }
       return descriptionCell
 }
 
 func tableView (_tableView:UITableView, heightForRowAt indexPath:IndexPath) ->UITableViewCell {

    switch indexPath.row {
        case2:
            if let descriptionCell = tableView.dequeueReusableCell(withIdentifier: "StoreDescriptionCell") as? StoreDescriptionCell {
                if self.isExpand { return CGFloat(self.newContentLabelHeight)}
            }
```



