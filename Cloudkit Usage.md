# Cloudkit 

Swift version: 3.0
Xcode version: 8.3

1. **To query a record by distance**
```Swift
    var nearbyTrolleys:[trolley]=[]
    let distance = 3000.0
    let locationPredicate = NSPredicate(format: "distanceToLocation:fromLocation:(%K, %@) < %f", "location", currentlocation, distance)
    let date = Date(timeInterval: -60 * 60 * 24 * 7, since: Date())
    let timePredicate = NSPredicate(format: "%K > %@", RecordField.creationDate.rawValue, date as CVarArg)
    let statusPredicate = NSPredicate(format: "%K = 0", RecordField.status.rawValue)
    let compoundPredicate = NSCompoundPredicate(type: .and, subpredicates: [timePredicate, locationPredicate, statusPredicate])
    let query = CKQuery(recordType: "trolley", predicate: compoundPredicate)
    let operation = CKQueryOperation(query: query)
    operation.resultsLimit = 50
    operation.desiredKeys = [RecordField.address.rawValue, RecordField.owner.rawValue, RecordField.creationDate.rawValue, RecordField.recordName.rawValue, RecordField.location.rawValue, RecordField.status.rawValue]
    
    operation.recordFetchedBlock = {(record:CKRecord) in
        nearbyTrolleys.append(self.recordToTrolley(arecord: record, currentlocation: currentlocation))
    }
    operation.queryCompletionBlock = {(_, error) in
        if error == nil {
            print ("retrieve nearby trolley successful \(nearbyTrolleys.count).")
            completion(true, nearbyTrolleys)
        } else {
            print (error)
            completion(false, nearbyTrolleys)
        }
    }
    publicdatabase.add(operation)
```

2. **Save image to local file**
```Swift
    func saveImageLocally() {
        let imageData: Data = UIImageJPEGRepresentation(noteImage.image!, 0.8)!
        let imageDirectoryPath = NSSearchPathForDirectoriesInDomains(.documentDirectory, .userDomainMask, true)[0] as NSString
        let imagename = "temp_image.jpg"
        let path = imageDirectoryPath.appendingPathComponent(imagename)
        imageURL = URL(fileURLWithPath: path)
        try? imageData.write(to: imageURL, options: [.atomic])
    }
```