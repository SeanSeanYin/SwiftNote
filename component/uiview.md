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



