# 二叉树的最大深度、最小深度

## 二叉树的最大深度

> 来源： [LeeCode 第 104 题](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree)
> 难度： 简单

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

说明: 叶子节点是指没有子节点的节点。

示例：

给定二叉树 `[3,9,20,null,null,15,7]`

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最大深度 3 。

### 思路

这个题思路比较简单，递归查找，每一层增加1, 然后加上左右子树选择最大的层数。

### 解题

```js
/**
 * 递归
 * @param {TreeNode} root
 * @return {number}
 */
var maxDepth = function(root) {
  if (root === null) return 0;
  return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
};

```

## 最小深度

> 来源： [LeeCode 第 111 题](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree)
> 难度： 简单

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

说明: 叶子节点是指没有子节点的节点。

示例:

给定二叉树 `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```

返回它的最小深度  2.

### 思路

这个题思路比较简单，递归查找左右子树最小的，然后比较。

### 解题

```js
var minDepth = function (root) {
  if(root === null) return 0;
  const left = minDepth(root.left);
  const right = minDepth(root.right);
  return (left === 0 || right === 0) ? left +right + 1 : 1 + Math.min(left, right);
}

```
