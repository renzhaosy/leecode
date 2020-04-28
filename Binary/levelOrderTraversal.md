# 二叉树的层序遍历

这一章是二叉树的层序遍历，但是主要是用到了栈的思想，所以这一章在栈和树两篇中都会有。

## 二叉树的层序遍历

> 来源： [LeeCode 第 102 题](https://leetcode-cn.com/problems/binary-tree-level-order-traversal)
> 难度： 中等
> 给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

示例：
二叉树：[3,9,20,null,null,15,7],

```
    3
   / \
  9  20
    /  \
   15   7
```

返回其层次遍历结果：

```
[
  [3],
  [9,20],
  [15,7]
]
```

### 实现

实现这里说两种，一种是树遍历中比较正常的广度优先遍历思想，第二种是利用深度优先遍历思想。

### 广度遍历实现

```js
/**
 * 利用广度优先遍历
 * @param {TreeNode} root
 * @return {number[][]}
 */
var levelOrder = function(root) {
  if (root === null) return [];
  const result = [];
  let list = [root];

  // 遍历当前层节点的数组
  while (list.length !== 0) {
    const len = list.length;
    const curList = [];
    const newList = [];
    for (let i = 0; i < len; i++) {
      const item = list[i];
      curList.push(item.val);
      // 将当前节点的左右节点加到新数组中，将作为下一个 while 循环的 list
      if (item.left !== null) {
        newList.push(item.left);
      }
      if (item.right !== null) {
        newList.push(item.right);
      }
    }
    list = newList; // 更新
    result.push(curList);
  }

  return result;
};
```

### 深度优先

利用深度优先遍历，不过将节点所在的层数 level 传入递归函数，确定在结果数组中元素的位置。

```js
var levelOrder = function(root) {
  if (root === null) return [];
  const result = [];

  // 将当前层数 level 作为参数
  const dfs = function(node, level) {
    if (node === null) return;
    if (!result[level]) {
      result[level] = [];
    }
    result[level].push(node.val);

    dfs(node.left, level + 1);
    dfs(node.right, level + 1);
  };

  dfs(root, 0);

  return result;
};
```

## 二叉树的锯齿形层次遍历

> 来源： [LeeCode 第 103 题](https://leetcode-cn.com/problems/binary-tree-zigzag-level-order-traversal)
> 难度： 中等

给定一个二叉树，返回其节点值的锯齿形层次遍历。（即先从左往右，再从右往左进行下一层遍历，以此类推，层与层之间交替进行）。

例如：
给定二叉树  [3,9,20,null,null,15,7],

```
    3
   / \
  9  20
    /  \
   15   7
```

返回锯齿形层次遍历如下：

```
[
  [3],
  [20,9],
  [15,7]
]
```

### 实现

```js
/**
 * @param {TreeNode} root
 * @return {number[][]}
 */
var zigzagLevelOrder = function(root) {
  if (root === null) return [];
  let list = [root];
  const result = [];
  let flag = 'left'; // start from left
  while (list.length !== 0) {
    const currList = [];
    const len = list.length;
    for (let i = 0; i < len; i++) {
      const item = list.shift();
      flag === 'left' ? currList.push(item.val) : currList.unshift(item.val);
      item.left !== null && list.push(item.left);
      item.right !== null && list.push(item.right);
    }
    flag = flag === 'left' ? 'right' : 'left';
    result.push(currList);
  }

  return result;
};
```
