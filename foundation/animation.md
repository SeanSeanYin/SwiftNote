# Animation

* **讓dismiss的時候，是從左往右退出**

```text
let transition: CATransition = CATransition()
transition.duration = 0.5
transition.timingFunction = CAMediaTimingFunction(name: kCAMediaTimingFunctionEaseInEaseOut)
transition.type = kCATransitionReveal
transition.subtype = kCATransitionFromLeft
self.view.window!.layer.add(transition, forKey: nil)
self.navigationController?.presentingViewController?.dismiss(animated: false, completion: nil)
```

