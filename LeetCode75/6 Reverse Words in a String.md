# Reverse words in a String

## Problem Statement:

Given an input string `s`, reverse the order of the  **words** .

A **word** is defined as a sequence of non-space characters. The **words** in `s` will be separated by at least one space.

Return *a string of the words in reverse order concatenated by a single space.*

**Note** that `s` may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.

**Example 1:**

<pre><strong>Input:</strong> s = "the sky is blue"
<strong>Output:</strong> "blue is sky the"
</pre>

**Example 2:**

<pre><strong>Input:</strong> s = "  hello world  "
<strong>Output:</strong> "world hello"
<strong>Explanation:</strong> Your reversed string should not contain leading or trailing spaces.
</pre>

**Example 3:**

<pre><strong>Input:</strong> s = "a good   example"
<strong>Output:</strong> "example good a"
<strong>Explanation:</strong> You need to reduce multiple spaces between two words to a single space in the reversed string.
</pre>

**Constraints:**

* `1 <= s.length <= 10<sup>4</sup>`
* `s` contains English letters (upper-case and lower-case), digits, and spaces `' '`.
* There is **at least one** word in `s`.

**Follow-up: **If the string data type is mutable in your language, can you solve it **in-place** with `O(1)` extra space?

## Solution:

#### Method 1:

```java
    class Solution {
        public boolean reverseWords(String s) {
            String[] strArray = s.split("\\s+");
            StringBuildersb = newStringBuilder();
            for ( inti = strArray.length - 1; i > 0; i--) {
                sb.append(strArray[i]).append(" ");
            }
            returnsb.append(strArray[0]).toString().trim();
        }
    }
```
