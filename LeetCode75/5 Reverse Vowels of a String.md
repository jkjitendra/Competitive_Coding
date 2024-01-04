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
            StringBuilder sb = new StringBuilder(s);
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

#### Method 2:

    class Solution {
        public boolean reverseVowels(String s) {
            int len = s.length();
            StringBuilder sb = new StringBuilder(s);
            String vowels = "aeiouAEIOU";
            int left = 0, j = len - 1;

            while (left < right) {

                 while (left < right && !vowels.contains(String.valueOf(s.charAt(left)))) {
                     left++;
                 }

                 while (right > left && !vowels.contains(String.valueOf(s.charAt(right)))) {
                    right--;
                 }

                 int temp = left;
                 sb.replace(left, left+1, String.valueOf(s.charAt(right)));
                 sb.replace(right, left+1, String.valueOf(s.charAt(temp)));

                 left++;
                 right--;
            }
            return sb.toString();
        }
    }

#### Method 3:

    class Solution {
        public boolean reverseVowels(String s) {
            int len = s.length();
            StringBuilder sb = new StringBuilder();
            Stack`<Character>` charStack = new Stack();

            for (int i = 0; i < len; i++) {
                char c = s.charAt(i);
                if (!isVowel(c)) {
                    stack.push(c);
                }
            }

            for (int i = 0; i < len; i++) {
                char c = s.charAt(i);
                if (!isVowel(c)) {
                    sb.append(c);
                } else {
                    sb.append(stack.pop());
                }
            }
            return sb.toString();
        }

        private boolean isVowel(char c) {
            if(c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u' ||
               c == 'A' || c == 'E' || c == 'I' || c == 'O' || c == 'U') {
                return true;
            }
            return false;
        }
    }

#### Method 4:

    class Solution {
        public boolean reverseVowels(String s) {
            boolean[] vowels = new boolean[128];

            //mark true at the Ascii index position of every vowel
            for (charc:"aeiouAEIOU".toCharArray()) {
                vowels[c] = true;
            }

            char[] cs = s.toCharArray();
            int left = 0, right = cs.length - 1;

            while (left < right) {

                while (left < right && !vowels[charArray[left]]) {
                    left++;
                }

                while (left < right && !vowels[charArray[right]]) {
                    right--;
                }

                if (left < right) {
                    chartempChar = charArray[left];
                    charArray[left] = charArray[right];
                    charArray[right] = tempChar;
                    left++;
                    right--;
                }
            }
            returnString.valueOf(charArray);
        }
    }
