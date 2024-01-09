# Maximum Number of Vowels in a Substring of Given Length

## Problem Statement:

Given a string `s` and an integer `k`, return *the maximum number of vowel letters in any substring of *`s`* with length *`k`.

**Vowel letters** in English are `'a'`, `'e'`, `'i'`, `'o'`, and `'u'`.

**Example 1:**

<pre><strong>Input:</strong> s = "abciiidef", k = 3
<strong>Output:</strong> 3
<strong>Explanation:</strong> The substring "iii" contains 3 vowel letters.
</pre>

**Example 2:**

<pre><strong>Input:</strong> s = "aeiou", k = 2
<strong>Output:</strong> 2
<strong>Explanation:</strong> Any substring of length 2 contains 2 vowels.
</pre>

**Example 3:**

<pre><strong>Input:</strong> s = "leetcode", k = 3
<strong>Output:</strong> 2
<strong>Explanation:</strong> "lee", "eet" and "ode" contain 2 vowels.
</pre>

**Constraints:**

* `1 <= s.length <= 10<sup>5</sup>`
* `s` consists of lowercase English letters.
* `1 <= k <= s.length`


## Solution:

#### Method 1:

    class Solution {
        public int maxVowels(String s, int k) {
            int n = s.length();
            if (n < k) return 0;
            int countOfVowel = 0, i = 0;
            for (; i < k; i++) {
                countOfVowel += isChar(s.charAt(i));
            }
            int maxNoOfVowel = countOfVowel;
            int currentIndex = k;
            while (currentIndex < n) {
                countOfVowel += isChar(s.charAt(currentIndex));
                countOfVowel -=  isChar(s.charAt(currentIndex-k));
                maxNoOfVowel = Math.max(maxNoOfVowel, countOfVowel);
                currentIndex++;
            }
            return maxNoOfVowel;
        }
        private int isChar(char c) {
            if(c == 'a' || c == 'e' || c == 'i' || c == 'o' || c == 'u') {
                return1;
            }
            return 0;
        }
    }

#### Method 2:

    class Solution {
        public int maxVowels(String s, int k) {
            int n = s.length();
            if (n < k) return 0;
            int currentIndex = 0, indexLeft = 0;
            int maxNoOfVowel = 0, countNoOfVowel = 0;
            byte[] byteOfString = s.getBytes();
            byte[] vowel = newbyte[123];
            vowel['a'] = vowel['e'] = vowel['u'] = vowel['i'] = vowel['o'] = 1;
            while (currentIndex < k) {
                countNoOfVowel += vowel[byteOfString[currentIndex++]];
            }
            maxNoOfVowel = countNoOfVowel;
            while (currentIndex < n) {
                countNoOfVowel += vowel[byteOfString[currentIndex++]] - vowel[byteOfString[indexLeft++]];
                if (countOfVowel > maxNoOfVowel) {
                    maxNoOfVowel = countNoOfVowel;
                }
                if (maxNoOfVowel == k){
                    return k;
                }
            }
            return maxNoOfVowel;
        }
    }
