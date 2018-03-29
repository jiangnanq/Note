# Summary of Push notification

1. **Request to authorization**
  * Add below code to Appdedelegate
    ```Swift
      UNUserNotificationCenter.current().delegate = self
      UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { (authorized, error) in
          if authorized {
              DispatchQueue.main.async {
                  application.registerForRemoteNotifications()
              }
          }
      }
    ```
2. **Add below code to handle notification when app in background**
  ```Swift
      func userNotificationCenter(_ center: UNUserNotificationCenter, willPresent notification: UNNotification, withCompletionHandler completionHandler: @escaping (UNNotificationPresentationOptions) -> Void) {
        completionHandler([.alert, .sound])
      }
  ```
