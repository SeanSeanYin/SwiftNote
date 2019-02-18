# UIImageView

* **讓UIImageView可以被點選的方式**

```text
let tap = UITapGestureRecognizer(target: self, action: #selector(imageViewCanBeClicked))
imageView.addGestureRecognizer(tap)
imageView.isUserInteractionEnabled = true
```

* **計算圖片大小**

```text
let imgData: NSData = NSData(data: UIImageJPEGRepresentation((image), 1)!)
let imageSize: Int = imgData.length
print("\(book.bookDetails.name) size of image in KB: %f ", Double(imageSize) / 1024.0)
```

