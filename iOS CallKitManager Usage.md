# How to use CallKitManager with Swift Language

1. **Add below line in the head**
  ```Swift
  import CallKit
  let extensionIdentifier:String = "Your extension identifier"
  ```
2. **To check the enable status of extension**
  ```Swift
  func checkEnableStatus() {
        let globalQueue = DispatchQueue.global()
        globalQueue.async {
            self.callmanager.getEnabledStatusForExtension(withIdentifier: extensionIdentifier, completionHandler: {(enablestatus: CXCallDirectoryManager.EnabledStatus, error:Error?) in
                if error == nil {
                    switch enablestatus {
                    case .disabled:
                        self.enableStatus = false
                    case .enabled:
                        self.enableStatus = true
                    case .unknown:
                        self.enableStatus = false
                    }
                    self.delegate?.didUpdateEnableStatus(status: self.enableStatus)
                }
            })
        }
    }
  ```
3. **To reload phone data of extension**
  ```Swift
    func reloadData() {
        let globalQueue = DispatchQueue.global()
        globalQueue.async {
            self.callmanager.reloadExtension(withIdentifier: extensionIdentifier, completionHandler: {(error:Error?) in
                var status:Bool = false
                if error == nil {
                    status = true
                    print ("load phone number data successful.")
                } else {
                    print ("error when reload phone data.")
//                    print (error?.localizedDescription)
                }
                self.delegate?.didReloadPhoneData(status: status)
            })
        }
    }
  ```