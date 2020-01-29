# Swift写算法

开始了博客之旅，从用Swift写算法开始，从最基础的排序开始吧

## 1、冒泡排序

**冒泡排序**（英語：**Bubble Sort**）又稱為**泡式排序**，是一種簡單的[排序算法](https://zh.wikipedia.org/wiki/排序算法)。它重複地走訪過要排序的[數列](https://zh.wikipedia.org/wiki/数列)，一次比較兩個元素，如果他們的順序錯誤就把他們交換過來。走訪數列的工作是重複地進行直到沒有再需要交換，也就是說該數列已經排序完成。這個算法的名字由來是因為越小的元素會經由交換慢慢「浮」到數列的頂端。

冒泡排序對![n](https://wikimedia.org/api/rest_v1/media/math/render/svg/a601995d55609f2d9f5e233e36fbe9ea26011b3b)個項目需要[O](https://zh.wikipedia.org/wiki/大O符号)(![n^{2}](https://wikimedia.org/api/rest_v1/media/math/render/svg/ac9810bbdafe4a6a8061338db0f74e25b7952620))的比較次數，且可以[原地](https://zh.wikipedia.org/wiki/原地算法)排序。儘管這個演算法是最簡單瞭解和實作的排序算法之一，但它對於包含大量的元素的數列排序是很沒有效率的。

冒泡排序演算法的運作如下：

1. 比較相鄰的元素。如果第一個比第二個大，就交換他們兩個。
2. 對每一對相鄰元素作同樣的工作，從開始第一對到結尾的最後一對。這步做完後，最後的元素會是最大的數。
3. 針對所有的元素重複以上的步驟，除了最後一個。
4. 持續每次對越來越少的元素重複上面的步驟，直到沒有任何一對數字需要比較。

了解了原理之后咱们通过代码来实现一下：

```swift
func bubbleSort(_ input:inout [Int]){
  guard input.count > 1 else {
    return
  }
  for i in 0..<(input.count - 1) {
    for j in 0..<(input.count - i - 1) {
      if input[j] > input[j+1] {
        input.swapAt(j, j+1)
      }
    }
  }
}
```

1. 先判断一下极限情况，如果数组中没有元素，则直接返回；
2. 然后开始进行遍历，相邻的两个元素比较，如果前边的比后边的大，进行交换；
3. 一层遍历只能将最大的元素沉底，所以需要for嵌套；

我们考虑一下，如果原数组是本来就大致有序的情况，用上述的代码进行排序，时间复杂度不变，所以我们还要增加特殊情况，我们想，如果有一次遍历中，数组中没有任何两个元素进行交换位置，是不是就表示已经有序了，所以代码如下

```swift
func bubbleSort(_ input:inout [Int]){
  guard input.count > 1 else {
    return
  }
  for i in 0..<(input.count - 1) {
    var exchanged = false
    for j in 0..<(input.count - i - 1) {
      if input[j] > input[j+1] {
        input.swapAt(j, j+1)
        exchanged = true
      }
    }
    if !exchanged {
      break
    }
  }
}
```

