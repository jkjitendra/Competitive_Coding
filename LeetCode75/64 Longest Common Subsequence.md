# Longest Common Subsequence

## Problem Statement:

Given two strings `text1` and `text2`, return *the length of their longest  **common subsequence** . *If there is no  **common subsequence** , return `0`.

A **subsequence** of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.

* For example, `"ace"` is a subsequence of `"abcde"`.

A **common subsequence** of two strings is a subsequence that is common to both strings.

**Example 1:**

<pre><strong>Input:</strong> text1 = "abcde", text2 = "ace" 
<strong>Output:</strong> 3  
<strong>Explanation:</strong> The longest common subsequence is "ace" and its length is 3.
</pre>

**Example 2:**

<pre><strong>Input:</strong> text1 = "abc", text2 = "abc"
<strong>Output:</strong> 3
<strong>Explanation:</strong> The longest common subsequence is "abc" and its length is 3.
</pre>

**Example 3:**

<pre><strong>Input:</strong> text1 = "abc", text2 = "def"
<strong>Output:</strong> 0
<strong>Explanation:</strong> There is no such common subsequence, so the result is 0.
</pre>

**Constraints:**

* `1 <= text1.length, text2.length <= 1000`
* `text1` and `text2` consist of only lowercase English characters.

## Solution:

#### Method 1:

```java
class Solution {
  public int longestCommonSubsequence(String text1, String text2) {
    int m = text1.length();
    int n = text2.length();
    int[][] dp = new int[m + 1][n + 1];
  
    for (int i = 1; i <= m; i++) {
      for (int j = 1; j <= n; j++) {
        if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
          dp[i][j] = dp[i - 1][j - 1] + 1;
        } else {
          dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
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
  public int longestCommonSubsequence(String text1, String text2) {
    if(text1.equals(text2)){
      return text1.length();
    }
    if(text2.length() > text1.length()) {
      return longestCommonSubsequence(text2, text1);
    }
    char[] s1 = text1.toCharArray();
    char[] s2 = text2.toCharArray();

    int[] prev = new int[s2.length + 1];
    int[] curr = new int[s2.length + 1];

    for (int i = 0; i < s1.length; i++) {
      for (int j = 0; j < s2.length; j++) {
        if (s1[i] == s2[j]) {
          curr[j +1] = prev[j] + 1;
        }else{
          curr[j + 1] = Math.max(curr[j], prev[j+1]);
        }
      }
      int[] temp = prev;
      prev = curr;
      curr = temp;
    }
    return prev[prev.length - 1];
  }
}
```
