# PagingCollectionView
The simplest way to make your collection view pagination

[![License: MIT](https://img.shields.io/badge/license-MIT-green.svg?style=flat)](https://github.com/Jigneshmayani90/PagingCollectionView/blob/main/LICENSE)
[![Platform](https://img.shields.io/cocoapods/p/PagingTableView.svg?style=flat)](https://github.com/Jigneshmayani90/PagingCollectionView/tree/main/RRPagingCollectionView/PagingCollectionView)
[![Swift 5.1](https://img.shields.io/badge/Swift-5.1-orange.svg?style=flat)](https://developer.apple.com/swift/)

The simplest way to add paginate function to your collection view.  
All you have to do is just set your collection view class in the storyboard to `RRPagingCollectionView`, and implement the `RRPagingCollectionViewDelegate#paginate`

## Example
![alt text](https://github.com/Jigneshmayani90/PagingCollectionView/blob/main/sample.gif)

## Requirements

pod 'RxCocoa'

pod 'RxSwift'

pod 'RxGesture'

pod 'Kingfisher'

## Installation

#### Manually
1. Download the project.
2. Add `RRPagingCollectionView.swift`, `RRPagingCollectionViewDelegate.swift` & `RRLoadingFooter.swift` with necessary files in your project.
3. Congratulations!  

## Usage example

First set your collection view class in the storyboard to `RRPagingCollectionView`

<img src="sample.png" width="500" />

Then implement `paginate` function. If `isLoading` is set to true, an indicator is displayed at the bottom of the collection view. Otherwise, the indicator disappears and `UICollectionView.reloadData` is called.

```swift

//Create RRPagingCollectionView class CollectionView outlet and set storyboard file itself
@IBOutlet weak var collectionView: RRPagingCollectionView!

//set pagingDelegate in viewDidLoad method
collectionView.pagingDelegate = self

//Start paging animation while data load from server
// MARK: - PagingCollectionViewDelegate -
func paginateCtn(_ collectionView: RRPagingCollectionView, to page: Int) {
    if !collectionView.isLoading && totalDataCount > dataArray.count {
        collectionView.isLoading = true
        //API call for getting new data
    }
}

//Set loading CollectionView Loading Footer view
func collectionView(_ collectionView: UICollectionView, viewForSupplementaryElementOfKind kind: String, at indexPath: IndexPath) -> UICollectionReusableView {
    return collectionView.collectionView(collectionView, viewForSupplementaryElementOfKind: kind, at: indexPath)
}

func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, referenceSizeForHeaderInSection section: Int) -> CGSize {
    return collectionView.collectionView(collectionView, layout: collectionViewLayout, referenceSizeForHeaderInSection: section)
}

func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, referenceSizeForFooterInSection section: Int) -> CGSize {
    return collectionView.collectionView(collectionView, layout: collectionViewLayout, referenceSizeForFooterInSection: section)
}

//Stop paging animation after get API response
collectionView.reloadData()
collectionView.isLoading = false

```
To run the example project, clone the repo, and run pod install from the Example directory first.

## APIs

| Name | Type | Description |
|---|---|---|
| `pagingDelegate` | `RRPagingCollectionViewDelegate` | Delegate pagination processing |
| `currentPage` | `Int` | Returns the current page |
| `isLoading` | `Bool` | Shows and hides the loading indicator. Reload collection view data after loading |
| `reset()` | `Void` | Return page to 0 and call `paginate` function |

## Contribute 

We would love you for the contribution to **PagingCollectionView**, check the ``LICENSE`` file for more info.


## License

[PagingCollectionView](https://github.com/Jigneshmayani90/PagingCollectionView/tree/main/RRPagingCollectionView/PagingCollectionView) is available under the MIT license. See the [LICENSE](https://github.com/Jigneshmayani90/PagingCollectionView/blob/main/LICENSE) file for more info.
