# Swift写算法

开始了博客之旅，从用Swift写算法开始，从最基础的排序开始吧

## 1、冒泡排序

冒泡排序是一种简单的排序算法。它重复地走访过要排序的数列，一次比较两个元素，如果它们的顺序错误就把它们交换过来。走访数列的工作是重复地进行直到没有再需要交换，也就是说该数列已经排序完成。这个算法的名字由来是因为越小的元素会经由交换慢慢“浮”到数列的顶端。

算法描述：

1. 比较相邻的元素。如果第一个比第二个大，就交换它们两个；
2. 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对，这样在最后的元素应该会是最大的数；
3. 针对所有的元素重复以上的步骤，除了最后一个；
4. 重复步骤1~3，直到排序完成。

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

## 2、快速排序

快速排序的基本思想：通过一趟排序将待排记录分隔成独立的两部分，其中一部分记录的关键字均比另一部分的关键字小，则可分别对这两部分记录继续进行排序，以达到整个序列有序。

算法描述：

1. 从数列中挑出一个元素，称为 “基准”（pivot）；
2. 重新排序数列，所有元素比基准值小的摆放在基准前面，所有元素比基准值大的摆在基准的后面（相同的数可以到任一边）。在这个分区退出之后，该基准就处于数列的中间位置。这个称为分区（partition）操作；
3. 递归地（recursive）把小于基准值元素的子数列和大于基准值元素的子数列排序。

实现：

```swift
func quickQort(arr:inout [Int], left:Int, right:Int){
    var partitionIndex = 0
    if left < right {
        partitionIndex = partition(arr: &arr, left: left, right: right)
        quickQort(arr: &arr, left: left, right: partitionIndex - 1)
        quickQort(arr: &arr, left: partitionIndex + 1, right: right)
    }
}

func partition(arr:inout [Int], left:Int, right:Int) -> Int{
    let pivot = left
    var index = pivot + 1
    for i in index...right {
        if arr[i] < arr[pivot] {
            arr.swapAt(i, index)
            index += 1
        }
    }
    arr.swapAt(pivot, index - 1)
    return index - 1
}
```

