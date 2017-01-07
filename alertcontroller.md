* #### AlertSheet
```
@IBAction func showSortSheet(sender: AnyObject) {

    let sortMenu = UIAlertController(title: nil, message: "Sort by", preferredStyle: .ActionSheet)

    let wifiAction = UIAlertAction(title: "Wifi", style: .Default, handler: nil)
    let cheapAction = UIAlertAction(title: "Cheap", style: .Default, handler: nil)
  
    sortMenu.addAction(wifiAction)
    sortMenu.addAction(cheapAction)
    self.presentViewController(sortMenu, animated: true, completion: nil)
  }
```