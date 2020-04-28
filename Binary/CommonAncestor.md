# 最小公共祖先

## 二叉树的最近公共祖先

> 来源： [LeeCode 第 236 题](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree)
> 难度： 中等

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉树:  root = [3,5,1,6,2,0,8,null,null,7,4]

![二叉搜索树](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/15/binarytree.png)

示例 1:

```
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出: 3
解释: 节点 5 和节点 1 的最近公共祖先是节点 3。
```

示例  2:

```
输入: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
输出: 5
解释: 节点 5 和节点 4 的最近公共祖先是节点 5。因为根据定义最近公共祖先节点可以为节点本身。
```

说明:

- 所有节点的值都是唯一的。
- p、q 为不同节点且均存在于给定的二叉树中。

### 思路

利用树遍历的思想：
首先如果当前节点等于 p 或者 q ，因为一个节点也可以是它自己的祖先，则表示当前节点是 p 或者 q 的最近的公共祖先。
否则，遍历左子树，在左子树中寻找，然后遍历右子树。如果两个子树中都没有找到则代表当前节点是 p 和 q 的最近公共祖先。
否则，判断左子树结果和右子树结果，哪个不为空，则哪个就是。

### 解题

```js
/**
 * @param {TreeNode} root
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */
var lowestCommonAncestor = function(root, p, q) {
  // 因为一个节点也可以是它自己的祖先
  // 所以如果root等于p或者q则最近祖先为root
  if (root === null || root === p || root === q) return root;
  // 递归在左、右子树中寻找
  const left = lowestCommonAncestor(root.left, p, q);
  const right = lowestCommonAncestor(root.right, p, q);
  // 如果左右子树的结果都为null, 则代表当前节点root为最近公共祖先
  if (left !== null && right !== null) {
    return root;
  } else {
    // 否则为左右子树的结果中的一个
    return left === null ? right : left;
  }
};
```

## 二叉搜索树的最近公共祖先

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉搜索树:  root = [6,2,8,0,4,7,9,null,null,3,5]

![二叉搜索树的最近公共祖先](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/14/binarysearchtree_improved.png)

示例 1:

```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
输出: 6
解释: 节点 2 和节点 8 的最近公共祖先是 6。
```

示例 2:

```
输入: root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
输出: 2
解释: 节点 2 和节点 4 的最近公共祖先是 2, 因为根据定义最近公共祖先节点可以为节点本身。
```

说明:

所有节点的值都是唯一的。
p、q 为不同节点且均存在于给定的二叉搜索树中。

> 来源： [LeeCode 第 235 题](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree)
> 难度： 中等

### 思路

同样这道题可以用到上一题的方法来查找，不过由于二叉搜索树的特性

二叉搜索树（排序二叉树）：空树或者具有以下特征的树

1. 左子树上所有结点的值均小于它的根结点的值
2. 右子树上所有结点的值均大于它的根结点的值
3. 以此类推，左子树、右子树也分别为二叉搜索树

可以通过比较root和p、q的值得比较，快速确定最小公共祖先的位置。

如果p、q 的值小于root,则最小公共祖先在左子树中，
如果p、q 的值大于root,则最小公共祖先在右子树中，
如果p、q 的值一个大于root,一个小于root,则表示p、q 一个在root的左边，一个在root的右边，则最小公共祖先为root。

### 解题

```js
/**
 * @param {TreeNode} root
 * @param {TreeNode} p
 * @param {TreeNode} q
 * @return {TreeNode}
 */
var lowestCommonAncestor = function(root, p, q) {
  // 因为一个节点也可以是它自己的祖先
  // 所以如果root等于p或者q则最近祖先为root
  if(root === null || root === p || root === q) return root;
  // 判断
  if (p.val < root.val && q.val < root.val) {
    return lowestCommonAncestor(root.left, p, q);
  } else if (p.val > root.val && q.val > root.val) {
    return lowestCommonAncestor(root.right, p, q);
  }
  return root;
};

```
