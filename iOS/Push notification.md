
## Remote push notification

1. Request to authorization
  Add below code to Appdedelegate

```swift
  UNUserNotificationCenter.current().delegate = self
  UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (authorized, error) in
      if authorized {
          DispatchQueue.main.async {
              application.registerForRemoteNotifications()
          }
      }
  }
```

1. Add below code to handle notification when app in background

```swift
    func userNotificationCenter(_ center: UNUserNotificationCenter, willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (UNNotificationPresentationOptions) -> Void) {
      completionHandler([.alert, .sound])
    }
```


