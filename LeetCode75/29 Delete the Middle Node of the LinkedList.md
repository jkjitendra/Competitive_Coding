# Delete the Middle Node of the LinkedList

## Problem Statement:

You are given the `head` of a linked list. **Delete** the  **middle node** , and return *the* `head`  *of the modified linked list* .

The **middle node** of a linked list of size `n` is the `⌊n / 2⌋<sup>th</sup>` node from the **start** using  **0-based indexing** , where `⌊x⌋` denotes the largest integer less than or equal to `x`.

* For `n` = `1`, `2`, `3`, `4`, and `5`, the middle nodes are `0`, `1`, `1`, `2`, and `2`, respectively.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/11/16/eg1drawio.png)

<pre><strong>Input:</strong> head = [1,3,4,7,1,2,6]
<strong>Output:</strong> [1,3,4,1,2,6]
<strong>Explanation:</strong>
The above figure represents the given linked list. The indices of the nodes are written below.
Since n = 7, node 3 with value 7 is the middle node, which is marked in red.
We return the new list after removing this node. 
</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/11/16/eg2drawio.png)

<pre><strong>Input:</strong> head = [1,2,3,4]
<strong>Output:</strong> [1,2,4]
<strong>Explanation:</strong>
The above figure represents the given linked list.
For n = 4, node 2 with value 3 is the middle node, which is marked in red.
</pre>

**Example 3:**

![](https://assets.leetcode.com/uploads/2021/11/16/eg3drawio.png)

<pre><strong>Input:</strong> head = [2,1]
<strong>Output:</strong> [2]
<strong>Explanation:</strong>
The above figure represents the given linked list.
For n = 2, node 1 with value 1 is the middle node, which is marked in red.
Node 0 with value 2 is the only node remaining after removing node 1.</pre>

**Constraints:**

* The number of nodes in the list is in the range `[1, 10<sup>5</sup>]`.
* `1 <= Node.val <= 10<sup>5</sup>`

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
  public ListNode deleteMiddle(ListNode head) {
    if (head.next == null) return null;
    ListNode slowPointer = head;
    ListNode fastPointer = head.next.next;  
    while (fastPointer != null && fastPointer.next != null) {
      slowPointer = slowPointer.next;
      fastPointer = fastPointer.next.next;
    }
    slowPointer.next = slowPointer.next.next;
    return head;
  }
}
```
