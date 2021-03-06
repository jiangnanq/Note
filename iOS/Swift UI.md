# Swift UI

1. UIButton

Add target to UIButton.
	
```swift
button.addTarget(self, action: #selector(MyClass.buttonTapped),
                forControlEvents: .TouchUpInside)
```

Add bar button and its action.

```swift
let barbutton = UIBarButtonItem(title: "save", style: UIBarButtonItemStyle.Plain, 
    target: self, action: #selector(saveAlbum))
self.navigationItem.rightBarButtonItem = barbutton
```

2. Navigation bar usage
Add bar button and its action
	
```swift
let barbutton = UIBarButtonItem(title: "save", style: UIBarButtonItemStyle.Plain, 
target: self, action: #selector(saveAlbum))
self.navigationItem.rightBarButtonItem = barbutton
```

3. Alert controller usage

```swift
func reportSpamMail() {
    let alertController = UIAlertController(title: "Report", message: "Report spam number", preferredStyle: .alert)
    
    let sendAction = UIAlertAction(title: "Report", style: .default, handler: {(_) -> Void in
        let receipients = [self.mailAddress]
        let subject = "From sgCallerID"
        let messagebody = ""
        
        let mailVC = self.configureMail(receipients: receipients, subject: subject, messageBody: messagebody)
        if MFMailComposeViewController.canSendMail() {
            self.present(mailVC, animated: true, completion: nil)
        }
    })
    
    let cancelAction = UIAlertAction(title: "Cancel", style: .default, handler: nil)
    alertController.addAction(sendAction)
    alertController.addAction(cancelAction)
    
    present(alertController, animated: true, completion: nil)
    
}
	```

4. Push viewController

```swift
let storyboard = UIStoryboard(name: "ContentDelivery", bundle: nil)
let webViewController = storyboard.instantiateViewControllerWithIdentifier("ContentDeliveryWebViewController") as! ContentDeliveryWebViewController
webViewController.url = url
webViewController.title = content.key
self.navigationController?.pushViewController(webViewController, animated: true)
```

5. Present viewController

```swift
func toNextViewController() {
  let storyboard = UIStoryboard(name: "Main", bundle: nil)
  var nextVc:UIViewController
  if let a = AVUser.currentUser() {
      nextVc = storyboard.instantiateViewControllerWithIdentifier("tabbar")
  } else {
      nextVc = storyboard.instantiateViewControllerWithIdentifier("login")
  }
  self.window?.rootViewController = nextVc
}
```

6. UISwitch usage

Toggle UISwitch status

```swift
@IBAction func toggleAlarm(_ sender:AnyObject) {
    if alarmSwitch.isOn {
        mute = false
        alarmSwitch.setOn(mute, animated: true)
    } else {
        mute = true
        alarmSwitch.setOn(mute, animated: true)
    }
}
```

7. Animation usage

Simple blink animation.

```swift
      if isBlink {
        cell.textLabel?.textColor = UIColor.red
        UIView.animate(withDuration: 1.0, delay: 0.0, options: [.allowUserInteraction, .repeat], animations: {
            cell.textLabel?.alpha = 0.5
        }, completion: { (finished:Bool) -> Void in
        })
    } else {
        UIView.animate(withDuration: 0.1, delay: 0.0, options: [.allowUserInteraction], animations: { 
            cell.textLabel?.alpha = 1.0
        }, completion: { (finished:Bool) -> Void in
        })
        cell.textLabel?.textColor = UIColor.white
    }
```

8. Add UIAlertController on ipad navigation bar button

After add barbutton item on navigation bar.

```swift
func menu() {
// The stype must be actionSheet, cannot set to alarm type!!!!
    let alertcontroller = UIAlertController(title: "Menu", message: "Select", preferredStyle: .actionSheet)
    let startAction = UIAlertAction(title: startstop, style: .default) { (_) -> Void in
        print ("Start button in Menu")
        self.startComm("a" as AnyObject)
    }
    let cancelaction = UIAlertAction(title: "Cancel", style: .default, handler: nil)
    alertcontroller.addAction(startAction)
    alertcontroller.addAction(cancelaction)
    alertcontroller.popoverPresentationController?.barButtonItem = self.navigationItem.rightBarButtonItem
    present(alertcontroller, animated: false, completion: nil)
}
```

9. Gradient color to view controller

Add gradient color to background

```swift
    let gradient = CAGradientLayer()
    gradient.frame = self.view.bounds
    gradient.colors = [UIColor.blue.cgColor, UIColor.green.cgColor]
    self.view.layer.insertSublayer(gradient, at: 0)
```

10. Add pop up menu on iPad collection view controller

```swift
func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath) {
   let vc = self.storyboard?.instantiateViewController(withIdentifier: "detailview") as! detailViewController
   vc.oneBed = dc.allBeds[indexPath.row]
   self.navigationController?.pushViewController(vc, animated: true)
   let i = (self.bedCollectionView.indexPathsForSelectedItems?[0].row)!
   let oneBed = self.dc.allBeds[i]
   let alertController = UIAlertController(title: "Bed", message: "Select", preferredStyle: .actionSheet)

   let selectAction = UIAlertAction(title: "Detail", style: .default) { (_) in
       let vc = self.storyboard?.instantiateViewController(withIdentifier: "detailview") as! detailViewController
       vc.oneBed = oneBed
       self.navigationController?.pushViewController(vc, animated: true)
   }

   let t = oneBed.isBypassed ? "Remove Bypass" : "Bypass"
   let bypassAction = UIAlertAction(title: t, style: .default) { (_) in
       print ("bypass alarm")
       oneBed.bypassTime = oneBed.isBypassed ? Date() : Date(timeInterval: 60 * 5, since: Date())
       self.bedCollectionView.reloadData()
   }

   let cancelAction = UIAlertAction(title: "Cancel", style: .default, handler: nil)

   alertController.addAction(selectAction)
   alertController.addAction(bypassAction)
   alertController.addAction(cancelAction)

   let popOver = alertController.popoverPresentationController
   popOver?.sourceView = collectionView.cellForItem(at: indexPath)
   popOver?.sourceRect = collectionView.cellForItem(at: indexPath)!.bounds
   popOver?.permittedArrowDirections = UIPopoverArrowDirection.any

   present(alertController, animated: true, completion: nil)
}
```
