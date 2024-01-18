# Reverse LinkedList

## Problem Statement:

Given the `head` of a singly linked list, reverse the list, and return  *the reversed list* .

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg)

<pre><strong>Input:</strong> head = [1,2,3,4,5]
<strong>Output:</strong> [5,4,3,2,1]
</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg)

<pre><strong>Input:</strong> head = [1,2]
<strong>Output:</strong> [2,1]
</pre>

**Example 3:**

<pre><strong>Input:</strong> head = []
<strong>Output:</strong> []
</pre>

**Constraints:**

* The number of nodes in the list is the range `[0, 5000]`.
* `-5000 <= Node.val <= 5000`


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
  public ListNode reverseList(ListNode head) {
    ListNode prev = null;
    ListNode current = head;
  
    if (head == null) return null;
    if (head.next == null) return head;
    while (current != null) {
      ListNode temp = current.next;
      current.next = prev;
      prev = current;
      current = temp;
    }
    return prev;
  }
}
```
