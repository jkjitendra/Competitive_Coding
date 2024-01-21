# Longest ZigZag Path in a Binary Tree

## Problem Statement:

You are given the `root` of a binary tree.

A ZigZag path for a binary tree is defined as follow:

* Choose **any **node in the binary tree and a direction (right or left).
* If the current direction is right, move to the right child of the current node; otherwise, move to the left child.
* Change the direction from right to left or from left to right.
* Repeat the second and third steps until you can't move in the tree.

Zigzag length is defined as the number of nodes visited - 1. (A single node has a length of 0).

Return  *the longest **ZigZag** path contained in that tree* .

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/01/22/sample_1_1702.png)

<pre><strong>Input:</strong> root = [1,null,1,1,1,null,null,1,1,null,1,null,null,null,1]
<strong>Output:</strong> 3
<strong>Explanation:</strong> Longest ZigZag path in blue nodes (right -> left -> right).
</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/01/22/sample_2_1702.png)

<pre><strong>Input:</strong> root = [1,1,1,null,1,null,null,1,1,null,1]
<strong>Output:</strong> 4
<strong>Explanation:</strong> Longest ZigZag path in blue nodes (left -> right -> left -> right).
</pre>

**Example 3:**

<pre><strong>Input:</strong> root = [1]
<strong>Output:</strong> 0
</pre>

**Constraints:**

* The number of nodes in the tree is in the range `[1, 5 * 10<sup>4</sup>]`.
* `1 <= Node.val <= 100`

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
  private int maxZigZagPath = 0;
  public int longestZigZag(TreeNode root) { 
    String direction = "";
    maxZigZag(root, direction, 0);
    return maxZigZagPath;
  }

  public void maxZigZag(TreeNode root, String direction, int count) {
    if (root == null) return;

    if (count > maxZigZagPath) maxZigZagPath = count;

    if (direction == "right" || direction == "") {
      maxZigZag(root.left, "left", count+1);
    } else {
      maxZigZag(root.left, "left", 1);
    }

    if (direction == "left" || direction == "") {
      maxZigZag(root.right, "right", count+1);
    } else {
      maxZigZag(root.right, "right", 1);
    }
  }
}
```
