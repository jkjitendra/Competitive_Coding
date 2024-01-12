# Determine If Two Strings are Close

## Problem Statement:

Two strings are considered **close** if you can attain one from the other using the following operations:

* Operation 1: Swap any two **existing** characters.
  * For example, `a<u>b</u>cd<u>e</u> -> a<u>e</u>cd<u>b</u>`
* Operation 2: Transform **every** occurrence of one **existing** character into another **existing** character, and do the same with the other character.
  * For example, `<u>aa</u>c<u>abb</u> -> <u>bb</u>c<u>baa</u>` (all `a`'s turn into `b`'s, and all `b`'s turn into `a`'s)

You can use the operations on either string as many times as necessary.

Given two strings, `word1` and `word2`, return `true`* if *`word1`* and *`word2`* are  **close** , and *`false`* otherwise.*

**Example 1:**

<pre><strong>Input:</strong> word1 = "abc", word2 = "bca"
<strong>Output:</strong> true
<strong>Explanation:</strong> You can attain word2 from word1 in 2 operations.
Apply Operation 1: "a<u>bc</u>" -> "a<u>cb</u>"
Apply Operation 1: "<u>a</u>c<u>b</u>" -> "<u>b</u>c<u>a</u>"
</pre>

**Example 2:**

<pre><strong>Input:</strong> word1 = "a", word2 = "aa"
<strong>Output:</strong> false
<strong>Explanation: </strong>It is impossible to attain word2 from word1, or vice versa, in any number of operations.
</pre>

**Example 3:**

<pre><strong>Input:</strong> word1 = "cabbba", word2 = "abbccc"
<strong>Output:</strong> true
<strong>Explanation:</strong> You can attain word2 from word1 in 3 operations.
Apply Operation 1: "ca<u>b</u>bb<u>a</u>" -> "ca<u>a</u>bb<u>b</u>"
<code>Apply Operation 2: "</code><u>c</u>aa<u>bbb</u>" -> "<u>b</u>aa<u>ccc</u>"
Apply Operation 2: "<u>baa</u>ccc" -> "<u>abb</u>ccc"
</pre>

**Constraints:**

* `1 <= word1.length, word2.length <= 10~5~`
* `word1` and `word2` contain only lowercase English letters.


## Solution:

#### Method 1:

```java
import java.util.Arrays;

class Solution {
  public boolean closeStrings(String word1, String word2) {
  
    int n = word1.length(), m = word2.length();
    if (n != m) return false;
    if (word1.equals(word2)) return true;

    int[] charArrayOfWord1 = new int[26];
    int[] charArrayOfWord2 = new int[26];

    for (char c: word1.toCharArray()) {
      charArrayOfWord1[c - 'a']++;
    }
    for (char c: word2.toCharArray()) {
      if (charArrayOfWord1[c - 'a'] == 0) return false;
      charArrayOfWord2[c - 'a']++;
    }
    Arrays.sort(charArrayOfWord1);
    Arrays.sort(charArrayOfWord2);

    return Arrays.equals(charArrayOfWord1, charArrayOfWord2);
  }
}
```


#### Method 2:

```java

```
