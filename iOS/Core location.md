# About core location

1. To show map in mapview

```swift
let initlocation:CLLocationCoordinate2D = CLLocationCoordinate2D(latitude: 1.34549354899945, longitude: 103.83823575360742)
let regionradius:CLLocationDistance = 30000
let region = MKCoordinateRegionMakeWithDistance(initlocation, regionradius, regionradius)
singaporeMap.setRegion(region, animated: true)
```

2. Init location manager

```swift
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
3. Add annotation on the map 

```swift
class busstop: nsobject, mkannotation  {
    var number, name, namechn, road, area: string
    var coordinate: cllocationcoordinate2d 
}

mapView.addAnnotations(allbusstops)
```
