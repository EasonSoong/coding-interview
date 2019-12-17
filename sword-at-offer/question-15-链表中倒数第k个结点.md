题目：输入一个链表，输出该链表中倒数第k个结点。为了符合大多数人的习惯，本体从1开始计数，即链表的尾结点是倒数第1个结点。例如一个链表有6个结点，从头结点开始它们的值依次是1、2、3、4、5、6。这个链表的倒数第3个结点是值为4的结点。

题解：看到题目第一反应是可以先遍历一遍链表得到长度，第二次遍历时就可以计算位置得出倒数第k个结点。但有没有更加好的方法呢？只遍历一次就达到目的？是的，我们可以选择定义两个指针，第一个指针从链表头部先向后走k-1步，第二个指针指向链表头部不动。然后第一个指针向后走一步，第二个指针跟着走，直到第一个指针到达链表的尾部，第一个指针指向的就是倒数第k个结点。

```js
const findKthNodeToTail = (head, k) => {
  if (!head || k === 0) {
    return null;
  }
  let pAhead = pBehind = head;
  for (let i = 0; i < k - 1; i++) {
    if (pAhead) {
      pAhead = pAhead.next;
    } else {
      throw new Error(`No ${k}th Node`);
    }
  }
  while (pAhead) {
    pAhead = pAhead.next;
    pBehind = pBehind.next;
  }
  return pBehind;
}
```
