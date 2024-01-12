# Is Subsequence

## Problem Statement:

Given two strings `s` and `t`, return `true`* if *`s`* is a **subsequence** of *`t`*, or *`false` * otherwise* .

A **subsequence** of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., `"ace"` is a subsequence of `"<u>a</u>b<u>c</u>d<u>e</u>"` while `"aec"` is not).

**Example 1:**

<pre><strong>Input:</strong> s = "abc", t = "ahbgdc"
<strong>Output:</strong> true
</pre>

**Example 2:**

<pre><strong>Input:</strong> s = "axc", t = "ahbgdc"
<strong>Output:</strong> false
</pre>

**Constraints:**

* `0 <= s.length <= 100`
* `0 <= t.length <= 10<sup>4</sup>`
* `s` and `t` consist only of lowercase English letters.

**Follow up:** Suppose there are lots of incoming `s`, say `s<sub>1</sub>, s<sub>2</sub>, ..., s<sub>k</sub>` where `k >= 10<sup>9</sup>`, and you want to check one by one to see if `t` has its subsequence. In this scenario, how would you change your code?

## Solution:

#### Method 1:

```java
    class Solution {
        public boolean isSubsequence(String s, String t) {
            if (s.length() == 0 && t.length() == 0) return true;
            if (s.length() > t.length()) return false;
            if (s.length() == t.length() && !s.equals(t)) return false;
            int count = 0;
            for (char charOfT: t.toCharArray()) {
                if (count < s.length() && s.charAt(count) == charOfT) {
                    count++;
                }
            }
            return count == s.length();
        }
    }
```
