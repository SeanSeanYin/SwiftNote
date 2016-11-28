# ViewContrller

* 新增背景圖片
  * ```self.view.backgroundColor = UIColor(patternImage: UIImage(named: "background.png"))```
* 用Label畫直線
  *  ```
     let lineView = UIView(frame: CGRect(x: 0, 
            y: label.bounds.size.height / 2,
            width: label.bounds.size.width,
            height: 1)) 
     lineView.backgroundColor = UIColor.blackColor();
     label.addSubview(lineView) ```
* 
