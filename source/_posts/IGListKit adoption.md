# IGListKit adoption

自從公司的App建構了新版的首頁之後，就在思考有沒有更能夠改善效能跟方便擴充性的架構。後來看到了FB的iOS Developer分享了這個Talk [(talk at try! Swift NYC)](https://realm.io/news/tryswift-ryan-nystrom-refactoring-at-scale-lessons-learned-rewriting-instagram-feed/)

---

對於原本的 `UICollectionView` or `UITableView` 來說，單一頁面存在多種不同 `layout`、`data type` 的設計，就不是一項可以讓設計簡潔、程式碼單純的功能。

依照過去類似的經驗，大概會是將每個 `item` / `cell` 的位置的檔案先用不同的 `model` 定義出來。例如：  

```
content : [
  card, card, list, card, ad, tag
]
```
每當決定每個 `row` 的類型時，透過 `content` 的內容去決定要產出什麼樣的 `item` ，這樣的設計，就叫做 `data driven` 的 `collectionView` pattern。

不過單純使用`content`決定UI的設計在原始的 `UICollectionView` or `UITableView` 上，會有幾個缺點。
1. 需要在多個位置判斷 `data type`，造成程式碼邏輯重複
2. 如果忘記 `register cell/item type`，則會造成crash，也增加系統風險
3. 在 `UICollectionView` 中插入 `Horizontal UICollectionView`，delegate需要獨立出來成為一個 `class / file`，而這樣的設計，也增加了閱讀的困難度

`IGListKit` 主要就是解決了以上的三個問題。

