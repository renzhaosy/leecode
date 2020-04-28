# 栈

## 有效括号

> 来源： [LeeCode 第 20 题](https://leetcode-cn.com/problems/valid-parentheses)
> 难度： 简单
> 给定一个只包括 '('，')'，'{'，'}'，'['，']'  的字符串，判断字符串是否有效。

有效字符串需满足：

左括号必须用相同类型的右括号闭合。
左括号必须以正确的顺序闭合。
注意空字符串可被认为是有效字符串。

示例 1:

```
输入: "()"
输出: true
```

示例  2:

```
输入: "()[]{}"
输出: true
```

示例  3:

```
输入: "(]"
输出: false
```

示例  4:

```
输入: "([)]"
输出: false
```

示例  5:

```
输入: "{[]}"
输出: true
```

### 思路

这道题利用栈的思想。

1. 首先设置一个`)}]`三种括号对应的 map
2. 遍历字符串将`({[`入栈。当遇到`)}]`时，
   - 先判断栈的长度，如果为 0 则表示没有对应的`({[`,则不是有效字符串。
   - stack.pop() 取出栈顶元素 和 当前右括号对应的最括号先比较：
     - 相等则表示这两个括号是一对，此时栈顶元素已更新，继续循环；
     - 否则，不相等则代表着当前右括号没有匹配的左括号，当前字符串无效。

### 解题

```js
const isValid = (s) => {
  const stack = [];
  const parenMap = {
    ')': '(',
    '}': '{',
    ']': '[',
  };

  for (let i = 0; i < s.length; i++) {
    const item = a[i];
    if (!parenMap[item]) {
      stack.push(item);
    } else if (!stack.length || parenMap[item] !== stack.pop()) {
      return false;
    }
  }

  return !stack.length;
};
```

