---
title: Summary of Swift 2
date: 2017-5-13
tags: iOS
---

# Summary of Swift development

The summary of Swift development. (Part 2)
Swift version: 3.0
Xcode version: 8.2.1

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
    {% codeblock lang:swift %}
    @IBAction func toggleAlarm(_ sender:AnyObject) {
        if alarmSwitch.isOn {
            mute = false
            alarmSwitch.setOn(mute, animated: true)
        } else {
            mute = true
            alarmSwitch.setOn(mute, animated: true)
        }
    }
    {% endcodeblock %}

2. <a name="Animation"></a> **Animation usage**
  * Simple blink animation.
  {% codeblock lang:swift %}
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
  {% endcodeblock %}

3. <a name="ArrayRemove"></a> **Remove an item from array**
  * Remove a string from string array.
  {% codeblock lang:swift %}
  blinkSensorName = Array(blinkSensorName.filter() {$0 != sName})
  {% endcodeblock %}

4. <a name="AlertController"></a> **Add UIAlertController on ipad navigation bar button**
  * After add barbutton item on navigation bar.
  {% codeblock lang:swift %}
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
  {% endcodeblock %}

5. <a name="NSPredicate"></a> **Simple example on how to use NSPredicate**
    * Query record from Realm database.
    {% codeblock lang:swift %}
        let dateformatter = DateFormatter()
        let dtstring = "2017-06-08 19:00:00"
        dateformatter.dateFormat = "YYYY-MM-dd HH:mm:ss"
        let dt:Date = dateformatter.date(from:dtstring)!
        let ht = "heartbeat"
        let predicate = NSPredicate(format: "timestamp >= %@ AND status != %@", dt as CVarArg, ht as CVarArg)
        let queryrecord = realm.objects(record.self).filter(predicate)
    {% endcodeblock %}

6. <a name="Motiondetect"></a> **Detect motion in viewcontroller**
    * Override func in viewcontroller.
    {% codeblock lang:swift %}
        override func motionEnded(motion: UIEventSubtype, withEvent event: UIEvent?) {
            if motion == .MotionShake {
                self.saveThisSong()
            }
        }
    {% endcodeblock %}

7. <a name="Playsound"></a> **Play system sound**
    * Play system sound once.
    {% codeblock lang:swift %}
        let systemSoudID:SystemSoundID = 1016
        AudioServicesPlaySystemSound(systemSoudID)
    {% endcodeblock %}

8. <a name="gradientcolor"></a> ** Gradient color to view controller**
    * Add gradient color to background
    {% codeblock lang:swift %}
        let gradient = CAGradientLayer()
        gradient.frame = self.view.bounds
        gradient.colors = [UIColor.blue.cgColor, UIColor.green.cgColor]
        self.view.layer.insertSublayer(gradient, at: 0)
    {% endcodeblock %}

9. <a name="userdefault"></a> ** Read and write user default setting**
    * Read and write user default
    {% codeblock lang:swift %}
        let defaults = UserDefaults.standard
        defaults.set(owner, forKey: RecordField.owner.rawValue)

        let defaults = UserDefaults.standard
        if let o = defaults.string(forKey: RecordField.owner.rawValue) {
            print (o)
        }
    {% endcodeblock %}

10. <a name="system notification"></a> ** How to add obersver for system notification **
    {% codeblock lang:swift %}
        NotificationCenter.default.addObserver(self, selector: #selector(ViewController.didBecomeActiveNotificaitonReceived), name: NSNotification.Name(rawValue: "UIApplicationDidBecomeActiveNotification"), object: nil)

        deinit {
            NotificationCenter.default.removeObserver(self, name: NSNotification.Name(rawValue: "UIApplicationDidBecomeActiveNotification"), object: nil)
        }
    {% endcodeblock %}