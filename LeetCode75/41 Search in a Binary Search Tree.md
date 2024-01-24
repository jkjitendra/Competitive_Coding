# Search in a Binary Search Tree

## Problem Statement:

You are given the `root` of a binary search tree (BST) and an integer `val`.

Find the node in the BST that the node's value equals `val` and return the subtree rooted with that node. If such a node does not exist, return `null`.

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/01/12/tree1.jpg)

<pre><strong>Input:</strong> root = [4,2,7,1,3], val = 2
<strong>Output:</strong> [2,1,3]
</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2021/01/12/tree2.jpg)

<pre><strong>Input:</strong> root = [4,2,7,1,3], val = 5
<strong>Output:</strong> []
</pre>

**Constraints:**

* The number of nodes in the tree is in the range `[1, 5000]`.
* `1 <= Node.val <= 10<sup>7</sup>`
* `root` is a binary search tree.
* `1 <= val <= 10<sup>7</sup>`

## Solution:

#### Method 1:

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
  public TreeNode searchBST(TreeNode root, int val) {
    if (root == null) return null;
    if (root.val == val) {
      return root;
    } else if (root.val > val) {
      return searchBST(root.left, val);
    } else {
      return searchBST(root.right, val);
    }
  }
}
```
