# Binary Tree Right Side View

## Problem Statement:

Given the `root` of a binary tree, imagine yourself standing on the **right side** of it, return  *the values of the nodes you can see ordered from top to bottom* .

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/02/14/tree.jpg)

<pre><strong>Input:</strong> root = [1,2,3,null,5,null,4]
<strong>Output:</strong> [1,3,4]
</pre>

**Example 2:**

<pre><strong>Input:</strong> root = [1,null,3]
<strong>Output:</strong> [1,3]
</pre>

**Example 3:**

<pre><strong>Input:</strong> root = []
<strong>Output:</strong> []
</pre>

**Constraints:**

* The number of nodes in the tree is in the range `[0, 100]`.
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
  public List<Integer> rightSideView(TreeNode root) {
    List<Integer> topToBottom = new ArrayList<>();
    int height = heightOfTree(root);
    for (int i = 0; i < height; i++) {
      topToBottom.add(-1);
    }
    addRightViewValue(root, topToBottom, 0);
    return topToBottom;
  }

  public void addRightViewValue(TreeNode root, List<Integer> topToBottom, int level) {
    if (root == null) return;
    topToBottom.set(level, root.val);
    addRightViewValue(root.left, topToBottom, level+1);
    addRightViewValue(root.right, topToBottom, level+1);
  }

  private int heightOfTree(TreeNode root) {
    if (root == null) return 0;
    int left = heightOfTree(root.left);
    int right = heightOfTree(root.right);
    return Math.max(left, right) + 1;
  }
}
```


#### Method 2:

```java
class Solution {
  int maxHeight = 0;
  public List<Integer> rightSideView(TreeNode root) {
    List<Integer> topToBottom = new ArrayList<>();
    addRightViewValue(root, topToBottom, 1);
    return topToBottom;
  }

  public void addRightViewValue(TreeNode root, List<Integer> topToBottom, int height) {
    if (root == null) return;
    if (maxHeight < height) {
      topToBottom.add(root.val);
      maxHeight = height;
    }
    addRightViewValue(root.right, topToBottom, height+1);
    addRightViewValue(root.left, topToBottom, height+1);
  }
}
```
