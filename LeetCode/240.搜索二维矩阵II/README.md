### 240.搜索二维矩阵II

---
编写一个高效的算法来搜索 m x n 矩阵 matrix 中的一个目标值 target。该矩阵具有以下特性：

每行的元素从左到右升序排列。
每列的元素从上到下升序排列。
示例:

现有矩阵 matrix 如下：
```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```
给定 target = 5，返回 true。

给定 target = 20，返回 false。

---

#### 二分查找

和“剑指offer-1.二维数组中的查找”一模一样

利用二分查找法，可以把二分值固定在右上角。

当target小于元素a[m][n]时，那么target必定在元素a所在行的左边,即n--；

当target大于元素a[m][m]时，那么target必定在元素a所在列的下边,即m++。

``` js
var searchMatrix = function(matrix, target) {
  let m = matrix.length
  if (m === 0) return false
  let n = matrix[0].length
  let i = 0
  let j = n - 1
  while (i < m && j >= 0) {
    if (matrix[i][j] < target) i++
    else if (matrix[i][j] > target) j--
    else return true
  }
  return false
};
```
