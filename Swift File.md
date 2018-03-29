# Summary of Swift file operation

1. **Save array to file**
    ```Swift
    @IBAction func saveToFile(_ sender: Any) {
        let filepath = NSSearchPathForDirectoriesInDomains(.documentDirectory, .userDomainMask, true)[0] as NSString
        let dateformatter = DateFormatter()
        dateformatter.dateFormat = "HH:mm:ss"
        let filename = dateformatter.string(from: Date()) + ".csv"
        let path = filepath.appendingPathComponent(filename)
        let fileurl = URL(fileURLWithPath: path)
        print (path)
        do {
            try logsToBeSave().write(to: fileurl, atomically: true, encoding: String.Encoding.utf8)
        } catch {
            print (error)
        }
    }
    ```

2. ** Read json data from file **
    ```Swift
    func readSensorDataFile(){
        let filepath = Bundle.main.path(forResource: "sensor", ofType: "json")
        var data:Data?
        do {
            data = try Data(contentsOf: URL(fileURLWithPath: filepath!), options: NSData.ReadingOptions.uncached)
        } catch {
            print ("error when read data file")
        }
        let sensorjson = JSON(Data: data!)
        for (key, sensortype):(String, JSON) in sensorjson {
            switch sensortype[0].stringValue {
            case SensorType.Motion.rawValue:
                allSensors[key] = Sensor(myid: key, gIP: gatewayIP, sType: .Motion)
            case SensorType.Magnet.rawValue:
                allSensors[key] =  Sensor(myid: key, gIP: gatewayIP, sType: .Magnet)
            default:
                allSensors[key] = Sensor(myid: key, gIP: gatewayIP, sType: .Switch)
            }
        }
    }
    ```
