# Maximum Level Sum of a Binary Tree

## Problem Statement:

Given the `root` of a binary tree, the level of its root is `1`, the level of its children is `2`, and so on.

Return the **smallest** level `x` such that the sum of all the values of nodes at level `x` is  **maximal** .

**Example 1:**

![](https://assets.leetcode.com/uploads/2019/05/03/capture.JPG)

<pre><strong>Input:</strong> root = [1,7,0,7,-8,null,null]
<strong>Output:</strong> 2
<strong>Explanation: </strong>
Level 1 sum = 1.
Level 2 sum = 7 + 0 = 7.
Level 3 sum = 7 + -8 = -1.
So we return the level with the maximum sum which is level 2.
</pre>

**Example 2:**

<pre><strong>Input:</strong> root = [989,null,10250,98693,-89388,null,null,null,-32127]
<strong>Output:</strong> 2
</pre>

**Constraints:**

* The number of nodes in the tree is in the range `[1, 10<sup>4</sup>]`.
* `-10<sup>5</sup> <= Node.val <= 10<sup>5</sup>`


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
  public int maxLevelSum(TreeNode root) {
    if (root.left == null && root.right == null) return 1;
    List<Integer> sumOfLevels = new ArrayList<>();
    sumofSameLevelValue(root, sumOfLevels, 0);
    int maxLevel = 0;
    for (int i = 1; i < sumOfLevels.size(); i++) {
      if (sumOfLevels.get(i) > sumOfLevels.get(maxLevel)) {
        maxLevel = i;
      }
    }
    return maxLevel + 1;
  }

  public void sumofSameLevelValue(TreeNode root, List<Integer> sumOfLevels, int level) {
    if (root == null) return;
    if (level == sumOfLevels.size()) sumOfLevels.add(0);

    sumOfLevels.set(level, sumOfLevels.get(level) + root.val);
    sumofSameLevelValue(root.left, sumOfLevels, level+1);
    sumofSameLevelValue(root.right, sumOfLevels, level+1);
  }
}
```



#### Method 2:

```java
  class Solution {

    private int[] totalSumInALevel = new int[100];
    private int maxLevel = 0;

    public int maxLevelSum(TreeNode root) {
      sumofSameLevelValue(root, 1);
      int maxSumLevel = 1;
      for (int level = 2; level <= maxLevel; ++level) {
        if (totalSumInALevel[maxSumLevel] < totalSumInALevel[level]) {
          maxSumLevel = level;
        }
      }
      return maxSumLevel;
    }

    private void sumofSameLevelValue(TreeNode root, int level) {
      if (root == null) return;

      maxLevel = Math.max(maxLevel, level);
      expandTheCapacityOfTotalSumInALevel(level);

      totalSumInALevel[level] += root.val;

      sumofSameLevelValue(root.left, level + 1);
      sumofSameLevelValue(root.right, level + 1);
    }

    private void expandTheCapacityOfTotalSumInALevel(int level) {
      if (level >= totalSumInALevel.length) {
        totalSumInALevel = Arrays.copyOf(totalSumInALevel, level * 2);
      }
    }
  }

```
