# Reverse Vowels of a String

## Problem Statement:


Given a string `s`, reverse only all the vowels in the string and return it.

The vowels are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`, and they can appear in both lower and upper cases, more than once.

**Example 1:**

<pre><strong>Input:</strong> s = "hello"
<strong>Output:</strong> "holle"
</pre>

**Example 2:**

<pre><strong>Input:</strong> s = "leetcode"
<strong>Output:</strong> "leotcede"
</pre>

**Constraints:**

* `1 <= s.length <= 3 * 10<sup>5</sup>`
* `s` consist of **printable ASCII** characters.


## Solution:

#### Method 1:

    class Solution {
        public boolean reverseVowels(String s) {
            int len = s.length();
            StringBuilder sb = new StringBuilder();
            String vowels = "aeiouAEIOU";
            int left = 0, j = len - 1;
            String leftChar = String.valueOf(s.charAt(left));
            String rightChar = String.valueOf(s.charAt(right));
            while (left < right) {
                 if (vowels.contains(leftChar)) {
                     if (vowels.contains(rightChar)) {
                         int temp = left;
                         sb.replace(left, left+1, String.valueOf(s.charAt(right)));
                         sb.replace(right, left+1, String.valueOf(s.charAt(temp)));
                         left++;
                         right--;
                     } else {
                             right--;
                       }
                 } else {
                       left++;
                   }
            return sb.toString();
        }
    }
