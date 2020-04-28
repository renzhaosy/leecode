# BST

二叉搜索树（排序二叉树）：空树或者具有以下特征的树

1. 左子树上所有结点的值均小于它的根结点的值
2. 右子树上所有结点的值均大于它的根结点的值
3. 以此类推，左子树、右子树也分别为二叉搜索树

## 验证二叉搜索树

> 难度： 中等
> 来源： [LeeCode 第 98 题](https://leetcode-cn.com/problems/validate-binary-search-tree)

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

节点的左子树只包含小于当前节点的数。
节点的右子树只包含大于当前节点的数。
所有左子树和右子树自身必须也是二叉搜索树。

示例  1:

```
输入:
    2
   / \
  1   3
输出: true
```

示例  2:

```
输入:
    5
   / \
  1   4
     / \
    3   6
输出: false
解释: 输入为: [5,1,4,null,null,3,6]。
     根节点的值为 5 ，但是其右子节点值为 4 。
```

### 思路

### 解题

```js
/**
 * Definition for a binary tree node.
 * function TreeNode(val) {
 *     this.val = val;
 *     this.left = this.right = null;
 * }
 */
/**
 * @param {TreeNode} root
 * @return {boolean}
 */
var isValidBST = function(root) {
  let prev = null;

  var helper = function(root) {
    if (!root) return true;
    if (!helper(root.left)) {
      return false;
    }
    if (prev && prev.val >= root.val) {
      return false;
    }
    prev = root;
    return helper(root.right);
  };
  return helper(root);
};
```

## 二叉搜索树的第k大节点
