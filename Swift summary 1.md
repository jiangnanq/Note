---
title: Summary of Swift 1
date: 2017-3-19
tags: iOS
---

1. [UIButton](#UIButton usage): To add action to UIButton
2. [Singleton class](#Singleton): How to create and use Singleton class
3. [Navigation bar](#Navigationbar): Navigation bar usage
4. [Alert Controller](#Alertcontroller): Alertcontroller usage
5. [Rate Apps in Appstore](#rateapp): Rate App in Appstore
6. [Select photo from album](#selectphoto): Select photo from album
7. [Background dispatch](#dispatch): Background dispatch queues
8. [Notification](#notification): Notification
9. [PushViewController](#pushviewcontroller): Push viewController
10. [PresentViewController](#presentviewcontroller): Present viewController
11. [RunTaskbyTimer](#timerTask): To start a timer task
12. [Check item in Array](#checkiteminarray): To check an item exist in Array


1. <a name="UIButton usage"></a> UIButton
  * Add target to UIButton.
```Swift
button.addTarget(self, action: #selector(MyClass.buttonTapped),
                forControlEvents: .TouchUpInside)
```
* Add bar button and its action.
```Swift
let barbutton = UIBarButtonItem(title: "save", style: UIBarButtonItemStyle.Plain, 
    target: self, action: #selector(saveAlbum))
self.navigationItem.rightBarButtonItem = barbutton
```

2. <a name="Singleton"></a> **Singleton class usage**
```Swift
class currentUserInfo {
    static let sharedCurrentUserInstance = currentUserInfo()
    var userRealName = ""
    private init() {}
}
let a = currentUserInfo.sharedCurrentUserInstance.userRealName
```

3. <a name="Navigationbar"></a> **Navigation bar usage**
  * Add bar button and its action
```Swift
let barbutton = UIBarButtonItem(title: "save", style: UIBarButtonItemStyle.Plain, 
target: self, action: #selector(saveAlbum))
self.navigationItem.rightBarButtonItem = barbutton
```

4. <a name="Alertcontroller"></a> **Alert controller usage**
```Swift
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

5. <a name="rateapp"></a> Rate app 
To rate the apps in the Appstore
```Swift
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
6. <a name="selectphoto"></a> **Select photo from libary**
```Swift
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
7. <a name="dispatch"></a> **Background dispatch queues**
```Swift
  DispatchQueue.global().async {
          print (message)
  }
```
8. <a name="notification"></a> **Notification**
```Swift
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
9. <a name="pushviewcontroller"></a> **Push viewController**
```Swift
let storyboard = UIStoryboard(name: "ContentDelivery", bundle: nil)
let webViewController = storyboard.instantiateViewControllerWithIdentifier("ContentDeliveryWebViewController") as! ContentDeliveryWebViewController
webViewController.url = url
webViewController.title = content.key
self.navigationController?.pushViewController(webViewController, animated: true)
```
10. <a name="presentviewcontroller"></a> **Present viewController**
```Swift
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
11. <a name="timerTask"></a> **To start a timer task**
```Swift
  var timer = Timer()
  self.timer = Timer.scheduledTimer(timeInterval: 5.0,
                              target: self,
                              selector: #selector(self.checkSensor),
                              userInfo: nil,
                              repeats: true)
  func checkSensor() {

  }
```
12. <a name="checkiteminarray"></a> ** To check an item exist in Array**
```Swift
if Array(sensorsid.keys).contains(messageid){
              processSensorMessage(json: json, index: messageid)
}

```
