# Count Good Nodes in Binary Tree

## Problem Statement:

Given a binary tree `root`, a node *X* in the tree is named **good** if in the path from root to *X* there are no nodes with a value *greater than* X.

Return the number of **good** nodes in the binary tree.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/04/02/test_sample_1.png)

<pre><strong>Input:</strong> root = [3,1,4,3,null,1,5]
<strong>Output:</strong> 4
<strong>Explanation:</strong> Nodes in blue are <strong>good</strong>.
Root Node (3) is always a good node.
Node 4 -> (3,4) is the maximum value in the path starting from the root.
Node 5 -> (3,4,5) is the maximum value in the path
Node 3 -> (3,1,3) is the maximum value in the path.</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/04/02/test_sample_2.png)

<pre><strong>Input:</strong> root = [3,3,null,4,2]
<strong>Output:</strong> 3
<strong>Explanation:</strong> Node 2 -> (3, 3, 2) is not good, because "3" is higher than it.</pre>

**Example 3:**

<pre><strong>Input:</strong> root = [1]
<strong>Output:</strong> 1
<strong>Explanation:</strong> Root is considered as <strong>good</strong>.</pre>

**Constraints:**

* The number of nodes in the binary tree is in the range `[1, 10^5]`.
* Each node's value is between `[-10^4, 10^4]`.


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
  private int count = 0;
  public int goodNodes(TreeNode root) {
    int X = root.val;
    checkForX(root, X);
    return count;
  }

  public void checkForX(TreeNode root, int X) {
    if (root == null) return;
    if (root.val >= X) {
      count++;
      X = root.val;
    }
    checkForX(root.left, X);
    checkForX(root.right, X);
  }
}
```


#### Method 2:

```java
class Solution {
  private int count = 0;
  public int goodNodes(TreeNode root) {
    checkForX(root, root.val);
    return count;
  }

  public void checkForX(TreeNode root, int X) {
    if (root.val >= X) {
      count++;
    }
    if (root.left != null) {
      checkForX(root.left, Math.max(root.val, X));
    }
    if (root.right != null) {
      checkForX(root.right, Math.max(root.val, X));
    }
  }
}
```
