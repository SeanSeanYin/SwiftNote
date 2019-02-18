# Auto Layout

### 當使用Constraint來限制View的Size時，想要在ViewDidLoad時變更View的Size的做法

```text
    override func viewWillLayoutSubviews() {
        // 這邊是view的bounds有任何變動時，都會呼叫的function
        super.viewWillLayoutSubviews()
    }
    
    override func viewDidLayoutSubviews() {
        // 這邊是最終畫出subview的地方，要改view的frame就在這邊改
        super.viewDidLayoutSubviews()
        if cellType != .none {
            containView.frame = CGRect.init(x: 0.0,
                                            y: switchButtonView.frame.maxY,
                                            width: containView.bounds.width,
                                            height: containViewHeightConstraint.constant)
        }
    }
```

## 

