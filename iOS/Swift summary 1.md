# Swift summary 1

1. UIButton
  * Add target to UIButton.

```swift
button.addTarget(self, action: #selector(MyClass.buttonTapped),
                forControlEvents: .TouchUpInside)
```

  * Add bar button and its action.

```swift
let barbutton = UIBarButtonItem(title: "save", style: UIBarButtonItemStyle.Plain, 
    target: self, action: #selector(saveAlbum))
self.navigationItem.rightBarButtonItem = barbutton
```

2. Singleton class usage

```swift
class currentUserInfo {
    static let sharedCurrentUserInstance = currentUserInfo()
    var userRealName = ""
    private init() {}
}
let a = currentUserInfo.sharedCurrentUserInstance.userRealName
```

3. Navigation bar usage
  Add bar button and its action

```swift
let barbutton = UIBarButtonItem(title: "save", style: UIBarButtonItemStyle.Plain, 
target: self, action: #selector(saveAlbum))
self.navigationItem.rightBarButtonItem = barbutton
```

4. Alert controller usage

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

5.  Rate app 
To rate the apps in the Appstore

```swift
func rateApp(appId:String, completion: @escaping ((_ success: Bool) ->())) {
    guard let url = URL(string: "itms-apps://itunes.apple.com/app/" + appId) else {
        completion(false)
        return
    }
    guard #available(iOS 10, *) else {
        completion(UIApplication.shared.openURL(url))
        return
    }
    UIApplication.shared.open(url, options: [:], completionHandler: completion)
}
```
6. Select photo from libary

```swift
func addPhoto() {
    imagePicker.allowsEditing = false
    imagePicker.sourceType = .PhotoLibrary
    imagePicker.delegate = self
    presentViewController(imagePicker, animated: true, completion: nil)
}
extension addPhotoViewController:UIImagePickerControllerDelegate,UINavigationControllerDelegate {
    func imagePickerController(picker: UIImagePickerController, didFinishPickingImage image: UIImage, editingInfo: [String : AnyObject]?) {
        self.selectPhoto[self.selectPhotoIndex] = image
        self.photoStatus[self.selectPhotoIndex] = true
        self.dismissViewControllerAnimated(true, completion: nil)
        newphotoCollectionView.reloadData()
    }
    
    func imagePickerControllerDidCancel(picker: UIImagePickerController) {
        dismissViewControllerAnimated(true, completion: nil)
    }
}
```
7. Background dispatch queues

```swift
  DispatchQueue.global().async {
          print (message)
  }
```
8. Notification

```swift
  // Define identifier
let notificationName = Notification.Name("NotificationIdentifier")

// Register to receive notification
NotificationCenter.default.addObserver(self, 
    selector: #selector(YourClassName.methodOfReceivedNotification), 
    name: notificationName, object: nil)

// Post notification
NotificationCenter.default.post(name: notificationName, object: nil)

// Stop listening notification
NotificationCenter.default.removeObserver(self, name: notificationName, object: nil);
```
9. Push viewController

```swift
let storyboard = UIStoryboard(name: "ContentDelivery", bundle: nil)
let webViewController = storyboard.instantiateViewControllerWithIdentifier("ContentDeliveryWebViewController") as! ContentDeliveryWebViewController
webViewController.url = url
webViewController.title = content.key
self.navigationController?.pushViewController(webViewController, animated: true)
```
10. Present viewController

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
11. To start a timer task

```swift
  var timer = Timer()
  self.timer = Timer.scheduledTimer(timeInterval: 5.0,
                              target: self,
                              selector: #selector(self.checkSensor),
                              userInfo: nil,
                              repeats: true)
  func checkSensor() {

  }
```
12. To check an item exist in Array

```swift
if Array(sensorsid.keys).contains(messageid){
              processSensorMessage(json: json, index: messageid)
}

```
