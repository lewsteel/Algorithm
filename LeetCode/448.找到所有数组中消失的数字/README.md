### 448.找到所有数组中消失的数字

---

给定一个范围在  1 ≤ a[i] ≤ n ( n = 数组大小 ) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 [1, n] 范围之间没有出现在数组中的数字。

您能在不使用额外空间且时间复杂度为O(n)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

示例:
```
输入:
[4,3,2,7,8,2,3,1]

输出:
[5,6]
```
---

#### 思路

参考评论区大神的思路

将所有正数 - 1 作为数组下标，置对应数组值为负值。那么，仍为正数的位置即为（未出现过）消失的数字。

举个例子：

原始数组：[4,3,2,7,8,2,3,1]

重置后为：[-4, -3, -2, -7, 8, 2, -3, -1]

结论：[8,2] 分别对应的index + 1为[5,6]（消失的数字）

``` js
var findDisappearedNumbers = function(nums) {
  const res = []
  for (const n of nums) {
    const index = Math.abs(n) - 1
    nums[index] = -1 * Math.abs(nums[index])
  }
  for (let i = 0; i < nums.length; i++) {
    if (nums[i] > 0) {
      res.push(i + 1)
    }
  }
  return res
};
```

再提供一种相似的思路

``` js
var findDisappearedNumbers = function(nums) {
  let len = nums.length
  const flag = Array(len).fill(true)
  for (let n of nums) {
    if (flag[n - 1]) flag[n - 1] = false
  }
  const res = []
  for (let i = 0; i < len; i++) {
    if (flag[i]) res.push(i + 1)
  }
  return res
};
```
