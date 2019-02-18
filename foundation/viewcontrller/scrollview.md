# ScrollView

* 不讓某個方向可以Drag

```text
    func scrollViewDidScroll(_ scrollView: UIScrollView) {
        if scrollView.contentOffset.y > 0 {
            scrollView.contentOffset.y = 0
        }
    }
```

