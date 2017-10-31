* #### Set shadow

```
    func setShadow(with color:CGColor = UIColor.black.cgColor, offset:CGSize = CGSize(width: 2, height: 2)) -> UIView {
        self.layer.shadowColor = color
        self.layer.shadowOpacity = 0.5
        self.layer.shadowOffset = offset
        self.layer.shadowRadius = 5
        self.layer.masksToBounds = false

        self.layer.shadowPath = UIBezierPath(rect: self.bounds).cgPath
        self.layer.shouldRasterize = true

        self.layer.rasterizationScale = UIScreen.main.scale

        // return 是為了可以調用鏈式呼叫        
        return self
    }
```

* #### 當有subview的的圖片超出view的圓角，造成無法顯示出圓角，就要對subview也設置圓角

```
        // 畫線，用subview的bounds，選擇哪些方向要顯示圓角，和圓角弧度
        let path = UIBezierPath(roundedRect: self.coverImageView.bounds, byRoundingCorners: [.topLeft, .topRight], cornerRadii: CGSize(width: 5.0, height: 5.0))
        let maskLayer = CAShapeLayer()
        maskLayer.path = path.cgPath
        // 將圓角的layer指定給subview的layer的mask
        self.coverImageView.layer.mask = maskLayer
```



