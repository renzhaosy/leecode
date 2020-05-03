# 数字

## 整数翻转

> 来源： [LeeCode 第 7 题](https://leetcode-cn.com/problems/reverse-integer)
> 难度： 简单

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

示例  1:

```
输入: 123
输出: 321
 示例 2:

输入: -123
输出: -321
```

示例 3:

```
输入: 120
输出: 21
注意:
```

假设我们的环境只能存储得下 32 位的有符号整数，则其数值范围为  [−231,  231 − 1]。请根据这个假设，如果反转后整数溢出那么就返回 0。

### 解题

这道题主要注意数值范围和负数。

```js
/**
 * @param {number} x
 * @return {number}
 */
var reverse = function(x) {
  if (x === 0) return x;

  const numStr = Math.abs(x)
    .toString()
    .split('')
    .reverse()
    .join('');
  const result = x < 0 ? -Number(numStr) : Number(numStr);

  if (result > Math.pow(2, 32) - 1 || result < Math.pow(2, 32)) {
    return 0;
  }
  return result;
};
```
