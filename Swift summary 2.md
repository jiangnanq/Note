---
title: Summary of Swift 2
date: 2017-5-13
tags: iOS
---

1. [UISwitch](#UISwitch): UISwitch usage
2. [Animation](#Animation): Animation usage
3. [Array remove item](#ArrayRemove): Remove item from Array
4. [Add UIAlertcontroller on iPad](#AlertController): Add alertcontroller on iPad
5. [NSPredicate](#NSPredicate): How to use NSPredicate
6. [Motiondetect](#Motiondetect): How to detect motion in viewcontroller
7. [Playsound](#Playsound): Play system sound
8. [Add gradient color](#gradientcolor): Add gradient color to view controller
9. [User default](#userdefault): Read/Write userdefault settings
10. [System notification](#system notification): How to oberserve system notification


1. <a name="UISwitch"></a> **UISwitch usage**
* Toggle UISwitch status
```Swift
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

1. <a name="Animation"></a> **Animation usage**
  * Simple blink animation.
```Swift
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

1. <a name="ArrayRemove"></a> **Remove an item from array**
  * Remove a string from string array.
```Swift
blinkSensorName = Array(blinkSensorName.filter() {$0 != sName})
```

1. <a name="AlertController"></a> **Add UIAlertController on ipad navigation bar button**
  * After add barbutton item on navigation bar.
```Swift
func menu() {
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

1. <a name="NSPredicate"></a> **Simple example on how to use NSPredicate**
    * Query record from Realm database.
```Swift
    let dateformatter = DateFormatter()
    let dtstring = "2017-06-08 19:00:00"
    dateformatter.dateFormat = "YYYY-MM-dd HH:mm:ss"
    let dt:Date = dateformatter.date(from:dtstring)!
    let ht = "heartbeat"
    let predicate = NSPredicate(format: "timestamp >= %@ AND status != %@", dt as CVarArg, ht as CVarArg)
    let queryrecord = realm.objects(record.self).filter(predicate)
```

1. <a name="Motiondetect"></a> **Detect motion in viewcontroller**
    * Override func in viewcontroller.
```Swift
    override func motionEnded(motion: UIEventSubtype, withEvent event: UIEvent?) {
        if motion == .MotionShake {
            self.saveThisSong()
        }
    }
```

1. <a name="Playsound"></a> **Play system sound**
    * Play system sound once.
```Swift
    let systemSoudID:SystemSoundID = 1016
    AudioServicesPlaySystemSound(systemSoudID)
```

1. <a name="gradientcolor"></a> ** Gradient color to view controller**
    * Add gradient color to background
```Swift
    let gradient = CAGradientLayer()
    gradient.frame = self.view.bounds
    gradient.colors = [UIColor.blue.cgColor, UIColor.green.cgColor]
    self.view.layer.insertSublayer(gradient, at: 0)
```

1. <a name="userdefault"></a> ** Read and write user default setting**
    * Read and write user default
```Swift
    let defaults = UserDefaults.standard
    defaults.set(owner, forKey: RecordField.owner.rawValue)

    let defaults = UserDefaults.standard
    if let o = defaults.string(forKey: RecordField.owner.rawValue) {
        print (o)
    }
```

1. <a name="system notification"></a> ** How to use system notification **
    - Add and post notification

    ```Swift
    let busstopNotification = Notification.Name("busStopNotification")
    let notifydict = ["number": self.number]
    NotificationCenter.default.post(name: busstopNotification, object: nil, userInfo: notifydict)
    ```

    - Observe the notification

    ```Swift
    NotificationCenter.default.addObserver(self, selector: #selector(updateSchedule), name: busstopNotification, object: nil)

    func updateSchedule(notification: NSNotification) {
        if let n = notification.userInfo?["number"] as? String {
        }
    }

    deinit {
        NotificationCenter.default.removeObserver(self, name: NSNotification.Name(rawValue: "UIApplicationDidBecomeActiveNotification"), object: nil)
    }
    ```