# 合并两个有序链表

## 非递归解题

思路： 思路比较简单，循环比较两个链表的节点，将小点的一个节点拿出来放到新的链表中。

```js
function merge(firstListHead, secondListHead) {
  // 合并两个有序链表
  if (firstListHead === null) {
    return secondListHead;
  }
  if (secondListHead === null) {
    return firstListHead;
  }

  let newNode = new Node(null); //哨兵节点
  let newHead = newNode;

  while (firstListHead && secondListHead) {
    if (firstListHead.value < secondListHead.value) {
      newNode.next = firstListHead;
      firstListHead = firstListHead.next;
    } else {
      newNode.next = secondListHead;
      secondListHead = secondListHead.next;
    }
    newNode = newNode.next;
  }
  
  if (firstListHead) {
    newNode.next = firstListHead;
  }

  if (secondListCur) {
    newNode.next = secondListCur
  }

  return newHead.next;
}


```

### 递归解题

思路同非递归的解法,只是递归的代码要更简练。

```js
function merge(firstListHead, secondListHead) {
  // 合并两个有序链表
  if (firstListHead === null) {
    return secondListHead;
  }
  if (secondListHead === null) {
    return firstListHead;
  }
  let newHead = new Node(null);
  if (firstListHead.value <= secondListHead.value) {
    newHead = firstListHead;
    newHead.next = merge(firstListHead.next, secondListHead);
  } else {
    newHead = secondListHead;
    newHead.next = merge(firstListHead, secondListHead.next)
  }

  return newHead;
}

```
