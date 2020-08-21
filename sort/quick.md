# 快速排序

快速排序的基本思想：通过一趟排序将要排序的数据分割成独立的两个部分，其中一部分的所有数据比另外一部分的所有数据都小，然后再对两个部分进行快速排序，直至所有数据排序完成。

## 快速排序原理

快速排序的原理非常简单：

- 在待排序的数据中找一个基准值，为了方便可以选择最后一个值为基准值。
- 然后遍历数组，将数组中小于基准值的元素放到基准值的左边，大于它对的元素放到右边，这时左右两个分区的元素就相对有序了。
- 接着对左右两个分区再重复 1、2 步的操作，一直到两个分区只有一个数为止。

> 时间复杂度 最坏 O(n^2)， 平均 O(nlogn)

## 实现

对数组 [3, 8, 4, 3, 5, 7, 9, 8, 2] 进行排序

```js
function quickSort(arr, left, right) {
  const len = arr.length;
  let leftIndex = left !== undefined ? left : 0;
  const rightIndex = right !== undefined ? right : len - 1; // 末尾元素下标

  if (leftIndex < rightIndex) {
    const pivotIndex = partition(arr, leftIndex, rightIndex); // 获取pivot位
    quickSort(arr, leftIndex, pivotIndex - 1);
    quickSort(arr, pivotIndex + 1, rightIndex);
  }

  return arr;
}

// 数组元素交换位置
function swap(arr, i, j) {
  const tmp = arr[i];
  arr[i] = arr[j];
  arr[j] = tmp;
}

// 分区操作
function partition(arr, left, right) {
  // left\right 为下角标
  let startIndex = left; // 记录左侧的起始位置
  const pivotVal = arr[right]; // 设定基准值 pivot

  // 维护一个 startIndex 指针，保证startIndex一直指向从左侧数第一个大于pivotVal的位置
  // 值和数组最后一位比较, 当小于pivotVal时， 值与startIndex的元素交换位置，startIndex + 1
  // 这样就维持了startIndex一直指向从左侧数第一个大于pivotVal的位置，并且 startIndex 之前的元素都小于pivotVal
  for (let i = left; i < right; i++) {
    if (arr[i] < pivotVal) {
      // 避免相同一个元素交换位置
      if (i !== startIndex) {
        swap(arr, i, startIndex);
      }
      startIndex++;
    }
  }

  // 基准值元素和大于它的第一个元素交换位置,这样左侧的都小于基准值，右侧的都大于基准值
  swap(arr, startIndex, right);
  return startIndex;
}

// 排序后： [2, 3, 3, 4, 5, 7, 8, 8, 9]
```

## 相关

求 TOP K
