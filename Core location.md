# Notes on Location Manager

1. **To show map in mapview**
```Swift
    let initlocation:CLLocationCoordinate2D = CLLocationCoordinate2D(latitude: 1.34549354899945, longitude: 103.83823575360742)
    let regionradius:CLLocationDistance = 30000
    let region = MKCoordinateRegionMakeWithDistance(initlocation, regionradius, regionradius)
    singaporeMap.setRegion(region, animated: true)
```

2. **Init location manager**
```Swift
    func initloactionManger() {
        locationmanager.delegate = self
        if CLLocationManager.locationServicesEnabled() {
            switch CLLocationManager.authorizationStatus() {
            case .notDetermined, .restricted, .denied:
                locationmanager.requestWhenInUseAuthorization()
            case .authorizedWhenInUse, .authorizedAlways:
                locationEnabled = true
                locationmanager.desiredAccuracy = kCLLocationAccuracyBest
                locationmanager.distanceFilter = 25
                locationmanager.startUpdatingLocation()
                currentlocation = nil
            default:
                return
            }
        }
    }
```
