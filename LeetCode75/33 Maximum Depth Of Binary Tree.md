# Maximum Depth of Binary Tree

## Problem Statement:

Given the `root` of a binary tree, return  *its maximum depth* .

A binary tree's **maximum depth** is the number of nodes along the longest path from the root node down to the farthest leaf node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg)

<pre><strong>Input:</strong> root = [3,9,20,null,null,15,7]
<strong>Output:</strong> 3
</pre>

**Example 2:**

<pre><strong>Input:</strong> root = [1,null,2]
<strong>Output:</strong> 2
</pre>

**Constraints:**

* The number of nodes in the tree is in the range `[0, 10<sup>4</sup>]`.
* `-100 <= Node.val <= 100`


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
  public int maxDepth(TreeNode root) {

    if (root == null) return 0;
    if (root.left == null && root.right == null) return 1;
    int maxLeftDepth = 0, maxRightDepth = 0;
    if (root.left != null)
      maxLeftDepth = 1 + this.maxDepth(root.left);
    else
      maxLeftDepth++;
    if (root.right != null)
      maxRightDepth = 1 + this.maxDepth(root.right);
    else
      maxRightDepth++;
    return Math.max(maxLeftDepth, maxRightDepth);
  }
}
```


#### Method 2:

```java

class Solution {
  public int maxDepth(TreeNode root) {

    if (root == null) return 0;
    if (root.left == null && root.right == null) return 1;
    int maxLeftDepth = this.maxDepth(root.left);
    int maxRightDepth = this.maxDepth(root.right);

    return 1 + Math.max(maxLeftDepth, maxRightDepth);
  }
}
```
