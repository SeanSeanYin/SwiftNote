* #### AlertSheet
```
@IBAction func showSortSheet(sender: AnyObject) {

    let sortMenu = UIAlertController(title: nil, message: "Sort by", preferredStyle: .ActionSheet)

    let wifiAction = UIAlertAction(title: "WIFI", style: .Default, handler: {
      (alert: UIAlertAction!) -> Void in
      println("File Deleted")
    })
    let saveAction = UIAlertAction(title: "Save", style: .Default, handler: {
      (alert: UIAlertAction!) -> Void in
      println("File Saved")
    })
    
    let cancelAction = UIAlertAction(title: "Cancel", style: .Cancel, handler: {
      (alert: UIAlertAction!) -> Void in
      println("Cancelled")
  
    optionMenu.addAction(deleteAction)
    optionMenu.addAction(saveAction)
    optionMenu.addAction(cancelAction)

    self.presentViewController(optionMenu, animated: true, completion: nil)
  }
```