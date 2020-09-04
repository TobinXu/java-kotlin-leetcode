fast 快指针提前走 n 步后，判断 fast.next 是否为 null ，即 fast 是否是最后一个节点，如果是，
则 head 为倒数第 n 个节点，此时问题可以简化为删除头节点；如果不是， fast = fast.next ，fast
再前进一步，slow 为倒数第 n+1 个节点，也解决了以上问题。

function removeNthFromEnd(head, n) {
  let [fast, slow] = [head, head];
  // fast先走n步
  while(--n) {
    fast = fast.next;
  }
  if (fast === null) return head.next; // 如果fast此时是尾结点即fast.next ===null, 则删除头结点
  fast = fast.next; // fast再向前走一步
  // 接下来fast\slow一起前进
  while(fast && fast.next) {
    fast = fast.next;
    slow = slow.next;
  }
  slow.next = slow.next.next;
  return head;
}

