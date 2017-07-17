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

  * 然後在 cellForRowAt 內更新Frame

  * functableView\(\_tableView:UITableView, cellForRowAt indexPath:IndexPath\) -&gt;UITableViewCell {

    switch indexPath.row {

    case2:

    ifletdescriptionCell = tableView.dequeueReusableCell\(withIdentifier:"StoreDescriptionCell"\)as?StoreDescriptionCell{



     descriptionCell.expandableLabel.isUserInteractionEnabled =true

     descriptionCell.expandableLabel.addGestureRecognizer\(tap\)

     descriptionCell.expandableLabel.sizeToFit\(\)



     print\("store's infomation :\\(store.storeObj.about\)"\)

    //設定字體大小

    self.setFont\(with: descriptionCell.contentLabel, in:16\)

    self.setFont\(with: descriptionCell.descriptionLabel, in:16\)



     descriptionCell.contentLabel.text = \(store.storeObj.about ==""\) ? NSLocalizedString\("na", comment:""\) : store.storeObj.about

  


     print\("font size:\\(descriptionCell.contentLabel.font.pointSize\) height:\\(descriptionCell.contentLabel.font.lineHeight\)"\)

    letheight = store.storeObj.about!.height\(withConstrainedWidth: UIScreen.main.bounds.width \*0.9, font: descriptionCell.contentLabel.font\)

    letwidth = store.storeObj.about!.width\(withConstraintedHeight: descriptionCell.contentLabel.font.lineHeight, font: descriptionCell.contentLabel.font\)



     print\("descriptionCell.contentLabel.frame.height:\\(descriptionCell.contentLabel.frame.height\)"\)

    ifheight &lt; \(descriptionCell.contentLabel.font.lineHeight \*3\) {

     descriptionCell.expandableLabel.isHidden =true

     }else{ descriptionCell.expandableLabel.isHidden =false}





    ifself.isExpand ==true{



     descriptionCell.expandableLabel.isEnabled =false

     descriptionCell.expandableLabel.text =""

     descriptionCell.contentLabel.numberOfLines =0

     descriptionCell.contentLabel.sizeToFit\(\)

    self.newContentLabelHeight = height + CGFloat\(50\) + descriptionCell.descriptionLabel.frame.height

     descriptionCell.contentView.frame = CGRect\(x:0.0, y:0.0, width: UIScreen.main.bounds.width \*0.9, height:self.newContentLabelHeight\)



    self.storeTableView.layoutIfNeeded\(\)

     }





    returndescriptionCell

     }



