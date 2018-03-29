# Summary of UITableViewController

##Basic usage
```Swift
 extension ViewController: UITableViewDelegate, UITableViewDataSource {
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        return messages.count
    }
    
    func numberOfSections(in tableView: UITableView) -> Int {
        return 1
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        let cell=tableView.dequeueReusableCell(withIdentifier: "message", for: indexPath)
        cell.textLabel?.text = messages[indexPath.row]
        return cell
    }
  }
```

1. Select cell and send data to next viewcontroller
```Swift
let vc = self.storyboard?.instantiateViewControllerWithIdentifier("studentDetailViewController") as? studentDetailViewController
vc?.newStudent = false
vc?.currentStudent = DataManager.copyStudent(Students[indexPath.row])
self.navigationController?.pushViewController(vc!, animated: true)  
```
2. Select cell and prepare to segue
```Swift
override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
    if segue.identifier == "showdetail" {
        let vc = segue.destination as! detailViewController
        vc.index = (bedCollectionView.indexPathsForSelectedItems?[0].row)!
    }
} 
```
3. Use custom cell in tableview controller
```Swift
  let cell = collectionView.dequeueReusableCellWithReuseIdentifier(reuseIdentifier, forIndexPath: indexPath) as! checkListCollectionViewCell
```
4. Delete row from tableview controller. Update UIView in other queue. Update tableview by use tableview.deleteRowAtIndexpath
```Swift
extension savedSongViewController:UITableViewDelegate {
  func tableView(savedSongTable: UITableView, canEditRowAtIndexPath indexPath: NSIndexPath) -> Bool {
      return true
  }
  
  func tableView(savedSongTable: UITableView, commitEditingStyle editingStyle: UITableViewCellEditingStyle, forRowAtIndexPath indexPath: NSIndexPath) {
      if editingStyle == .Delete {
          self.allSavedSongs.removeAtIndex(indexPath.row)
          self.savedSongs?.favoriteTracks.removeAtIndex(indexPath.row)
          self.savedSongs?.saveAllSongs()
          var selectIndex = [NSIndexPath]()
          selectIndex.append(indexPath)
          savedSongTable.deleteRowsAtIndexPaths(selectIndex, withRowAnimation: UITableViewRowAnimation.Fade)
          dispatch_async(dispatch_get_main_queue(), { () -> Void in
              self.savedSongTable?.reloadData()
          })            
      }
  }
}
```
5. Detect button/image was tapped in a cell (use protocol)
  [Link](http://candycode.io/how-to-properly-do-buttons-in-table-view-cells/)

6. Click a cell and popup alertcontroller
```Swift
func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath) {
    let i = indexPath.row
    print ("\(i)")
    let alertController = UIAlertController(title: "Bed", message: "Select", preferredStyle: .actionSheet)
    
    let selectAction = UIAlertAction(title: "Detail", style: .default) { (_) in
        print ("show detail")
    }
    let cancelAction = UIAlertAction(title: "Cancel", style: .default, handler: nil)
    alertController.addAction(selectAction)
    alertController.addAction(cancelAction)
    let popOver = alertController.popoverPresentationController
    popOver?.sourceView = collectionView.cellForItem(at: indexPath)
    popOver?.sourceRect = collectionView.cellForItem(at: indexPath)!.bounds
    popOver?.permittedArrowDirections = UIPopoverArrowDirection.any
    
    present(alertController, animated: true, completion: nil)
}
```