* #### 讓UIImageView可以被點選的方式

```
let tap = UITapGestureRecognizer(target: self, action: #selector(imageViewCanBeClicked))
imageView.addGestureRecognizer(tap)
imageView.isUserInteractionEnabled = true
```



