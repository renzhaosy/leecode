# 反转链表

首先了解一下链表中节点的结构.

```js
function ListNode(val) {
  this.val = val;
  this.next = null;
}
```

## 1. 简单的反转一个单链表

难度： 简单

翻转一个单链表。

示例:

```

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL

```

来源： [LeeCode 第 206 题](https://leetcode-cn.com/problems/reverse-linked-list/)

### 解题思路

这道题算是链表的经典题目。`思路简单`但是考验`代码的实现`。

主要思路是遍历整个数组，然后将节点的`next`指针指向它的前一个节点，应该注意的是`后续节点的保存`，确定`next`指针的位置。

### 非递归方案

```js
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function(head) {
  if (head === null) return null;
  let [prev, cur] = [null, head];
  while (cur) {
    // 关键： 保存下一个节点
    let tmp = cur.next;
    cur.next = prev; // 将当前节点的next指向前一个节点
    prev = cur; // 将当前节点作为下个循环的prev
    cur = tmp; // 将下一个节点作为下个循环的当前节点
    // 简化
    // [cur.next, prev, cur] = [prev, cur, cur.next]
  }
  return prev;
};
```

### 递归方案

思路在非递归的方案中已经很清楚，下边是递归方式的实现。

```js
var reverseList = function(head) {
  if (head === null) return null;

  var reverse = function(prev, cur) {
    if (cur === null) return prev;
    let tmp = cur.next;
    cur.next = prev;
    prev = cur;
    cur = tmp;
    return reverse(prev, cur);
  };
  return reverse(null, head);
};
```

## 2. 区间翻转

级别： 中等

翻转从位置 m 到 n 的链表。请使用一趟扫描完成翻转。

说明:
1 ≤ m ≤ n ≤ 链表长度。

示例:

```js
输入: 1->2->3->4->5->NULL, m = 2, n = 4
输出: 1->4->3->2->5->NULL
```

来源： [LeeCode 第 92 题](https://leetcode-cn.com/problems/reverse-linked-list-ii/)

### 思路

这道题是上一道题的延伸，思路还是同样的，需要注意的是保存`前后节点`。

### 非递归方案

```js

/**
 * @param {ListNode} head
 * @param {number} m
 * @param {number} n
 * @return {ListNode}
 */
var reverseBetween = function(head, m, n) {
  if (head === null) return head;
  if (m > n) return head;
  // 记录新链表的头部节点
  const newHead = new ListNode(null);
  newHead.next = head;
  let prev = newHead;

  for (let i = 0 ; i < m - 1; i++>) {
    prev = prev.next;
  }

  let front = prev; // 保存前节点 第m - 1个节点
  let tail = prev = prev.next; // 第m个节点  保存下来当做翻转之后的尾结点
  let cur = prev.next;

  const nums = m - n;
  for (let j = 0; j < nums; j++) {
    let tmp = cur.next;
    cur.next = prev;
    prev = cur;
    cur = tmp;
  }

  // 前节点的next指向翻转之后的头结点
  front.next = prev;
  // 翻转之后的尾结点的next指向cur节点（循环之后cur指向后边链表的第一个节点）
  tail.next = cur;
  return newHead.next;
};

```

### 递归方案

递归方案和非递归方案的区别在于对翻转区域的处理，更换为递归来处理

## 3. 两两交换链表中的节点

难度： 中等

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

你不能只是单纯的改变节点内部的值，而是需要实际的进行节点交换。

示例:

```
给定 1->2->3->4, 你应该返回 2->1->4->3.
```

来源： [LeeCode 第 92 题](https://leetcode-cn.com/problems/swap-nodes-in-pairs)

### 思路

首先创建一个哨兵节点 `newHead`。

newHead -> 1(head) -> 2 -> 3 -> 4 -> null;

(prev)
prev 指向将要翻转的两个节点的前节点，则 prev.next 和 prev.next.next 就是 node1 和 node2,分别保存为 first 和 second;
然后 fitst.next = second.next 、 second.next = first 、 prev.next = second 将 node1 和 node2 翻转，
再讲 prev 指针指向翻转之后的第二个节点 first。至此完成一次循环的翻转操作。
如图：

### 非递归

```js
var swapPairs = function(head) {
  let headNode = new ListNode(null); // 哨兵节点
  headNode.next = head;
  let prev = headNode;
  while (prev.next !== null && prev.next.next !== null) {
    let first = prev.next;
    let second = first.next;
    first.next = second.next;
    prev.next = second;
    second.next = first;
    prev = first;
  }
  return headNode;
};
```

### 递归方案

递归的话就不需要哨兵节点了，代码更简洁，实现如下

```js
var swapPairs = function(head) {
  if (head === null || head.next === null) {
    return head;
  }
  let node1 = head;
  let node2 = head.next;
  node1.next = swapPairs(node2.next);
  node2.next = node1;
  return node2;
};
```

### 4. K 个一组翻转链表

难度： 困难

给你一个链表，每  k  个节点一组进行翻转，请你返回翻转后的链表。

k  是一个正整数，它的值小于或等于链表的长度。

如果节点总数不是  k  的整数倍，那么请将最后剩余的节点保持原有顺序。

示例：

```
给你这个链表：1->2->3->4->5

当 k = 2 时，应当返回: 2->1->4->3->5

当 k = 3 时，应当返回: 3->2->1->4->5
```

说明：

你的算法只能使用常数的额外空间。
你不能只是单纯的改变节点内部的值，而是需要实际进行节点交换。

来源： [LeeCode 第 25 题](https://leetcode-cn.com/problems/reverse-nodes-in-k-group)

### 思路

思路和上一题类似，唯一的区别在于以两个为一组翻转和以 K 个为一组翻转。

### 递归

递归的话思路更清晰，思路见备注

```js
/**
 * @param {ListNode} head
 * @param {number} k
 * @return {ListNode}
 */
var reverseKGroup = function(head, k) {
  let p = head;

  // 先检测后边的节点能够构成一组
  for (let i = 0; i < k; i++) {
    if (p === null) return head; // 不能构成一组， 则返回头节点
    p = p.next;
  }

  let prev = null;
  let cur = (tail = head); // tail 保存头节点，翻转之后为尾结点

  for (let j = 0; j < k; j++) {
    let tmp = cur.next;
    cur.next = prev;
    prev = cur;
    cur = tmp;
  }

  // 循环完之后 cur 为后续链表的第一个节点
  // 递归反转后边的
  tail.next = reverseKGroup(cur, k);
  return prev;
};
```
