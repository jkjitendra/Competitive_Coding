# Edit Distance

## Problem Statement:

Given two strings `word1` and `word2`, return  *the minimum number of operations required to convert `word1` to `word2`* .

You have the following three operations permitted on a word:

* Insert a character
* Delete a character
* Replace a character

**Example 1:**

<pre><strong>Input:</strong> word1 = "horse", word2 = "ros"
<strong>Output:</strong> 3
<strong>Explanation:</strong> 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')
</pre>

**Example 2:**

<pre><strong>Input:</strong> word1 = "intention", word2 = "execution"
<strong>Output:</strong> 5
<strong>Explanation:</strong> 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')
</pre>

**Constraints:**

* `0 <= word1.length, word2.length <= 500`
* `word1` and `word2` consist of lowercase English letters.

## Solution:

#### Method 1:

```java
class Solution {
  public int minDistance(String word1, String word2) {
    int m = word1.length(), n = word2.length();
    int[][] dp = new int[m + 1][n + 1];

    for (int i = 0; i <= m; i++) dp[i][0] = i;
    for (int j = 0; j <= n; j++) dp[0][j] = j;

    for (int i = 1; i <= m; i++) {
      for (int j = 1; j <= n; j++) {
        if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
          dp[i][j] = dp[i - 1][j - 1];
        } else {
          dp[i][j] = 1 + Math.min(dp[i - 1][j - 1], Math.min(dp[i][j - 1], dp[i - 1][j]));
        }
      }
    }

    return dp[m][n];
  }
}
```

#### Method 2:

```java
class Solution {
  public int minDistance(String word1, String word2) {
    Integer[][] dp = new Integer[word1.length()][word2.length()];
    return minDistanceHelper(word1, word2, word1.length(), word2.length(), dp);
  }

  private int minDistanceHelper(String word1, String word2, int m, int n, Integer[][] dp) {
    if (m == 0) return n; // If word1 is empty, all characters of word2 need to be inserted
    if (n == 0) return m; // If word2 is empty, all characters of word1 need to be deleted

    // Check if result is already computed in dp table
    if (dp[m - 1][n - 1] != null) {
      return dp[m - 1][n - 1];
    }

    // If characters are equal, move diagonally without any operation
    if (word1.charAt(m - 1) == word2.charAt(n - 1)) {
      dp[m - 1][n - 1] = minDistanceHelper(word1, word2, m - 1, n - 1, dp);
    } else {
      int deleteCost = minDistanceHelper(word1, word2, m - 1, n, dp);
      int insertCost = minDistanceHelper(word1, word2, m, n - 1, dp);
      int replaceCost = minDistanceHelper(word1, word2, m - 1, n - 1, dp);

      dp[m - 1][n - 1] = 1 + Math.min(Math.min(deleteCost, insertCost), replaceCost);
    }

    return dp[m - 1][n - 1];
  }
}
```
