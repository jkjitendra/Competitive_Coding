# Delete Node in a BST

## Problem Statement:

Given a root node reference of a BST and a key, delete the node with the given key in the BST. Return  *the **root node reference** (possibly updated) of the BST* .

Basically, the deletion can be divided into two stages:

1. Search for a node to remove.
2. If the node is found, delete the node.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/09/04/del_node_1.jpg)

<pre><strong>Input:</strong> root = [5,3,6,2,4,null,7], key = 3
<strong>Output:</strong> [5,4,6,2,null,null,7]
<strong>Explanation:</strong> Given key to delete is 3. So we find the node with value 3 and delete it.
One valid answer is [5,4,6,2,null,null,7], shown in the above BST.
Please notice that another valid answer is [5,2,6,null,4,null,7] and it's also accepted.
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/04/del_node_supp.jpg"/>
</pre>

**Example 2:**

<pre><strong>Input:</strong> root = [5,3,6,2,4,null,7], key = 0
<strong>Output:</strong> [5,3,6,2,4,null,7]
<strong>Explanation:</strong> The tree does not contain a node with value = 0.
</pre>

**Example 3:**

<pre><strong>Input:</strong> root = [], key = 0
<strong>Output:</strong> []
</pre>

**Constraints:**

* The number of nodes in the tree is in the range `[0, 10<sup>4</sup>]`.
* `-10<sup>5</sup> <= Node.val <= 10<sup>5</sup>`
* Each node has a **unique** value.
* `root` is a valid binary search tree.
* `-10<sup>5</sup> <= key <= 10<sup>5</sup>`

**Follow up:** Could you solve it with time complexity `O(height of tree)`?


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
  public TreeNode deleteNode(TreeNode root, int key) {
    if (root == null) return null;

    if (key < root.val) {
      root.left = deleteNode(root.left, key);
    } else if (key > root.val) {
      root.right = deleteNode(root.right, key);
    } else {
      if (root.left == null) {
        return root.right;
      } else if (root.right == null) {
        return root.left;
      } else {
        TreeNode minValNode = inOrderSuccessor(root.right);
        root.val = minValNode.val;
        root.right = deleteNode(root.right, root.val);
      }
    }
    return root;
  }

  public TreeNode inOrderSuccessor(TreeNode rightTreeRoot) {
    while (rightTreeRoot.left != null) {
      rightTreeRoot = rightTreeRoot.left;
    }
    return rightTreeRoot;
  }
}
```
