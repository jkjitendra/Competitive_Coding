# Path Sum III

## Problem Statement:

Given the `root` of a binary tree and an integer `targetSum`, return *the number of paths where the sum of the values along the path equals* `targetSum`.

The path does not need to start or end at the root or a leaf, but it must go downwards (i.e., traveling only from parent nodes to child nodes).

**Example 1:**

![](https://assets.leetcode.com/uploads/2021/04/09/pathsum3-1-tree.jpg)

<pre><strong>Input:</strong> root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
<strong>Output:</strong> 3
<strong>Explanation:</strong> The paths that sum to 8 are shown.
</pre>

**Example 2:**

<pre><strong>Input:</strong> root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
<strong>Output:</strong> 3
</pre>

**Constraints:**

* The number of nodes in the tree is in the range `[0, 1000]`.
* `-10<sup>9</sup> <= Node.val <= 10<sup>9</sup>`
* `-1000 <= targetSum <= 1000`


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
  public int pathSum(TreeNode root, int targetSum) {
    Map<Long, Integer> sumOfNodes = new HashMap<>();
    sumOfNodes.put(0L,1);
    return totalPathEqualToSum(root, 0L ,targetSum, sumOfNodes);
  }

  public int totalPathEqualToSum(TreeNode root, long currentSum, int targetSum, Map<Long, Integer> sumOfNodes) {
    if (root == null) {
      return 0;
    }
    currentSum += root.val;
    int totalPaths = sumOfNodes.getOrDefault(currentSum - targetSum, 0);
    sumOfNodes.put(currentSum, sumOfNodes.getOrDefault(currentSum, 0) + 1);

    totalPaths += totalPathEqualToSum(root.left, currentSum, targetSum, sumOfNodes) + totalPathEqualToSum(root.right, currentSum, targetSum, sumOfNodes);
    sumOfNodes.put(currentSum, sumOfNodes.get(currentSum) - 1);
    return totalPaths;
  }

}
```
