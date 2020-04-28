# Loop

## 判断链表是否有环

#### 思路

利用快慢指针，快慢指针法是链表算法中常用的一种方法，通过两个步长不同的移动指针，可以帮助解决一些链表中的问题。
通常，慢指针每次移动一个节点，快指针每次移动两个节点，因此，二者的路径存在一个二倍的数学关系（偶数节点情况下）。

如果链表有环的话，快慢两个指针迟早会相遇，所以可以依次来判断链表上是否有环。

```js
function isLoop(head) {
  let slowNode = head;
  let fastNode = head;
  while( slowNode && fastNode && fastNode.next ) {
    slowNode = slowNode.next;
    fastNode = fastNode.next.next;
    if (slowNode === fastNode) {
      return true;
    }
  }
  return false;
}

```

## 寻找链表的中间节点

```js
  findMiddleNode(head) {
    // 利用快慢指针
    // 快慢指针法是链表算法中常用的一种方法，通过两个步长不同的移动指针，可以帮助解决一些链表中的问题。
    // 通常，慢指针每次移动一个节点，快指针每次移动两个节点，因此，二者的路径存在一个二倍的数学关系（偶数节点情况下）
    // slowNode, fastNode 为头部节点
    let newHead = new ListNode(null); // 哨兵节点
    newHead.next = head;
    let slowNode = newHead;
    let fastNode = newHead;

    while(fastNode !== null && fastNode.next !== null) {
      slowNode = slowNode.next;
      fastNode = fastNode.next.next;
    }

    // 运行到此处
    // 奇数节点： faseNode 为null， slowNode 为中间节点
    // 偶数节点： fastNode.next 为 null , slowNode 为中前节点 （前半段最后一个节点）
    return slowNode;
  }

```
