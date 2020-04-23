# n 数之和

## 001 两数之和（two-sum）

给定一个整数数组 nums 和一个目标值 target，请你在该数组中找出和为目标值的那 两个 整数，并返回他们的数组下标。
你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

示例:

```js
给定 nums = [2, 7, 11, 15], target = 9

因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

来源：  [LeeCode 第 1 题](https://leetcode-cn.com/problems/two-sum/submissions/)

### 解题

#### 2.1 for()

- 代码:

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
  for (let i = 0; i < nums.length; i++) {
    for (let j = i + 1; j < nums.length; j++) {
      if (nums[i] === target - nums[j]) {
        return [i, j];
      }
    }
  }
};
```

- 执行结果
  1. 输入:
     nums: [2,7,11,15]
     target: 9
  2. 输出: [0,1]

* 解题思路: 利用双重的 for 循环。

#### 2.2 数组 indexOf()

- 代码:

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
  if (!Array.isArray(nums) || typeof target !== "number") return;
  for (let i = 0, len = nums.length; i < len; i++) {
    if (
      nums.indexOf(target - nums[i]) > -1 &&
      nums.indexOf(target - nums[i]) !== i
    ) {
      return [i, nums.indexOf(target - nums[i])].sort((a, b) => a - b);
    }
  }
};
```

- 执行结果

  1. 输入:
     nums: [2,7,11,15]
     target: 9
  2. 输出: [0,1]

- 解题思路:
  1. Array.prototype.indexOf()方法返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1。
  2. 每个值只用一次
  3. Array.prototype.sort() 对索引值排序

#### 2.3 对象{}

- 代码:

```js
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var twoSum = function(nums, target) {
  if (!Array.isArray(nums) || typeof target !== "number") return;
  const hash = {};
  for (let i = 0, len = nums.length; i < len; i++) {
    let j = hash[target - nums[i]];
    if (j !== undefined && j !== i) {
      return [j, i];
    }
    hash[nums[i]] = i;
  }
};
```

- 执行结果

  1. 输入:
     nums: [2,7,11,15]
     target: 9
  2. 输出: [0,1]

- 解题思路:
  使用对象存储 nums 数组中的值和索引，通过判断 hash[target - nums[i]] 是否存在 hash 中，没有的话添加，有则直接返回[j, i]。
