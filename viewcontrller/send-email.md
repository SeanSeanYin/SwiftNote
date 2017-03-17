* 先 `import MessageUI`
* 再實作Delegate

```
extension AboutViewController:MFMailComposeViewControllerDelegate {
    
    func mailComposeController(_ controller: MFMailComposeViewController, didFinishWith result: MFMailComposeResult, error: Error?) {
        switch result {
            case .cancelled:
                print("Cancel")
            case .saved:
                print("Save")
            case .sent:
                print("Sent")
            case .failed:
                print("Failed")
            }
            controller.dismiss(animated: true, completion: nil)
    }
}
```

* 呼叫出Mail畫面

```
if MFMailComposeViewController.canSendMail() {

   let subject = "約約意見反應"
   let messageBody = "\n\n 機型：\(UIDevice.current.modelName)\n OS版本：\(UIDevice.current.systemVersion) "
   let recipients = ["kimiyin@gmail.com"]
   let mailController = MFMailComposeViewController()
   mailController.mailComposeDelegate = self
   mailController.setSubject(subject)
   mailController.setMessageBody(messageBody, isHTML: false)
   mailController.setToRecipients(recipients)
   self.present(mailController, animated: true, completion: nil)
}
```



