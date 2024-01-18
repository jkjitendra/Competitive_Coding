# Odd Even LinkedList

## Problem Statement:

Given the `head` of a singly linked list, group all the nodes with odd indices together followed by the nodes with even indices, and return  *the reordered list* .

The **first** node is considered  **odd** , and the **second** node is  **even** , and so on.

Note that the relative order inside both the even and odd groups should remain as it was in the input.

You must solve the problem in `O(1)` extra space complexity and `O(n)` time complexity.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/03/10/oddeven-linked-list.jpg)

<pre><strong>Input:</strong> head = [1,2,3,4,5]
<strong>Output:</strong> [1,3,5,2,4]
</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/03/10/oddeven2-linked-list.jpg)

<pre><strong>Input:</strong> head = [2,1,3,5,6,4,7]
<strong>Output:</strong> [2,3,6,7,1,5,4]
</pre>

**Constraints:**

* The number of nodes in the linked list is in the range `[0, 10<sup>4</sup>]`.
* `-10<sup>6</sup> <= Node.val <= 10<sup>6</sup>`

## Solution:

#### Method 1:

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
  public ListNode oddEvenList(ListNode head) {
    if(head == null || head.next == null){
      return head;
    }
    ListNode odd = head;
    ListNode even = head.next;
    ListNode enHead = even;
    while (even != null && even.next != null && odd != null && odd.next != null) {
      odd.next = even.next;
      odd = odd.next;
      even.next = odd.next;
      even = even.next;
    }
    odd.next = enHead;
    return head;
  }
}
```
