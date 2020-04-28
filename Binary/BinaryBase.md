# 基础

这篇是介绍一些树的基础

## 递归方式生成树

```js
/* 生成树 */
function TreeNode(val) {
  this.val = val;
  this.left = null;
  this.right = null;
}

function createBinaryTree(list) {
  if (!list.length) return null;
  const data = list.shift();
  if (data !== null) {
    const node = new TreeNode(data);
    node.left = createBinaryTree(list);
    node.right = createBinaryTree(list);
    return node;
  }
  return null;
}
```

## 树的遍历

### 前序遍历、中序遍历、后序遍历

前中后序指的是根结点在遍历过程中所在的顺序。

前序遍历： 根结点、左子节点、右子节点
中序遍历：左子节点、根结点、右子节点
后序遍历：左子节点、根结点、右子节点

```js
/* 前序遍历  打印 */
function preOrder(root) {
  if (root === null) return;
  console.log('前序遍历  ', root.val);
  preOrder(root.left);
  preOrder(root.right);
}

/* 中序遍历  打印 */
function inOrder(root) {
  if (root === null) return;
  inOrder(root.left);
  console.log('中序遍历  ', root.val);
  inOrder(root.right);
}

/* 后序遍历  打印 */
function backOrder(root) {
  if (root === null) return;
  backOrder(root.left);
  backOrder(root.right);
  console.log('后序遍历  ', root.val);
}

```

### 广度优先、深度优先
