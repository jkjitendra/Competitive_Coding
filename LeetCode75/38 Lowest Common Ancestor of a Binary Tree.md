# Lowest Common Ancestor of a Binary Tree

## Problem Statement:

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the [definition of LCA on Wikipedia](https://en.wikipedia.org/wiki/Lowest_common_ancestor): “The lowest common ancestor is defined between two nodes `p` and `q` as the lowest node in `T` that has both `p` and `q` as descendants (where we allow  **a node to be a descendant of itself** ).”

**Example 1:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

<pre><strong>Input:</strong> root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
<strong>Output:</strong> 3
<strong>Explanation:</strong> The LCA of nodes 5 and 1 is 3.
</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2018/12/14/binarytree.png)

<pre><strong>Input:</strong> root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
<strong>Output:</strong> 5
<strong>Explanation:</strong> The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
</pre>

**Example 3:**

<pre><strong>Input:</strong> root = [1,2], p = 1, q = 2
<strong>Output:</strong> 1
</pre>

**Constraints:**

* The number of nodes in the tree is in the range `[2, 10<sup>5</sup>]`.
* `-10<sup>9</sup> <= Node.val <= 10<sup>9</sup>`
* All `Node.val` are  **unique** .
* `p != q`
* `p` and `q` will exist in the tree.

## Solution:

#### Method 1:

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
  public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if (root == null || root == p || root == q) return root;
    TreeNode left = lowestCommonAncestor(root.left, p, q);
    TreeNode right = lowestCommonAncestor(root.right, p, q);
    if (right != null && left != null) return root;
    return left != null ? left : right;
  }
}
```
