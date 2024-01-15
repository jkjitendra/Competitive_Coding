# Decode String

## Problem Statement:

Given an encoded string, return its decoded string.

The encoding rule is: `k[encoded_string]`, where the `encoded_string` inside the square brackets is being repeated exactly `k` times. Note that `k` is guaranteed to be a positive integer.

You may assume that the input string is always valid; there are no extra white spaces, square brackets are well-formed, etc. Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, `k`. For example, there will not be input like `3a` or `2[4]`.

The test cases are generated so that the length of the output will never exceed `10<sup>5</sup>`.

**Example 1:**

<pre><strong>Input:</strong> s = "3[a]2[bc]"
<strong>Output:</strong> "aaabcbc"
</pre>

**Example 2:**

<pre><strong>Input:</strong> s = "3[a2[c]]"
<strong>Output:</strong> "accaccacc"
</pre>

**Example 3:**

<pre><strong>Input:</strong> s = "2[abc]3[cd]ef"
<strong>Output:</strong> "abcabccdcdcdef"
</pre>

**Constraints:**

* `1 <= s.length <= 30`
* `s` consists of lowercase English letters, digits, and square brackets `'[]'`.
* `s` is guaranteed to be **a valid** input.
* All the integers in `s` are in the range `[1, 300]`.


## Solution:

#### Method 1:

```java
  class Solution {
    public String decodeString(String s) {
      Stack<Integer> numStack = new Stack<>();
      Stack<Integer> indexStack = new Stack<>();
      StringBuilder decodedString = new StringBuilder();
      int num = 0;

      for (char c : s.toCharArray()) {
        if (Character.isDigit(c)) {
          num = num * 10 + c - '0';
        } else if (c == '[') {
          numStack.push(num);
          indexStack.push(decodedString.length());
          num = 0;
        } else if (c == ']') {
          int startIndex = indexStack.pop();
          int count = numStack.pop();
          String repeatStr = decodedString.substring(startIndex);
          while (count-- > 1) {
            decodedString.append(repeatStr);
          }
        } else {
          decodedString.append(c);
        }
      }
      return decodedString.toString();
    }
  }
```
