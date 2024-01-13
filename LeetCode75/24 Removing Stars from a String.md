# Removing Stars from a String

## Problem Statement:

You are given a string `s`, which contains stars `*`.

In one operation, you can:

* Choose a star in `s`.
* Remove the closest **non-star** character to its  **left** , as well as remove the star itself.

Return  *the string after **all** stars have been removed* .

**Note:**

* The input will be generated such that the operation is always possible.
* It can be shown that the resulting string will always be unique.

**Example 1:**

<pre><strong>Input:</strong> s = "leet**cod*e"
<strong>Output:</strong> "lecoe"
<strong>Explanation:</strong> Performing the removals from left to right:
- The closest character to the 1<sup>st</sup> star is 't' in "lee<strong><u>t</u></strong>**cod*e". s becomes "lee*cod*e".
- The closest character to the 2<sup>nd</sup> star is 'e' in "le<strong><u>e</u></strong>*cod*e". s becomes "lecod*e".
- The closest character to the 3<sup>rd</sup> star is 'd' in "leco<strong><u>d</u></strong>*e". s becomes "lecoe".
There are no more stars, so we return "lecoe".</pre>

**Example 2:**

<pre><strong>Input:</strong> s = "erase*****"
<strong>Output:</strong> ""
<strong>Explanation:</strong> The entire string is removed, so we return an empty string.
</pre>

**Constraints:**

* `1 <= s.length <= 10<sup>5</sup>`
* `s` consists of lowercase English letters and stars `*`.
* The operation above can be performed on `s`.

## Solution:

#### Method 1:

```java
  class Solution {
    public String removeStars(String s) {
      int n = s.length();
      Stack lifo = new Stack();
      String sb = "";
      for (int i = 0; i < n; i++) {
        if (s.charAt(i) == '*' && i-1 >= 0) {
          lifo.pop();
        } else {
          lifo.push(s.charAt(i));
        }
      }
      for (int i = 0; i < lifo.size(); i++) {
        sb += lifo.get(i);
      }
      return sb;
    }
  }
```


#### Method 2:

```java
  class Solution {
    public String removeStars(String s) {
      int len = s.length();
      byte[] result = new byte[len];
      int resultIndex = 0;
      for (int i = 0; i < len; i++) {
        if (s.charAt(i) == '*') {
          if (resultIndex > 0) {
              resultIndex--;
          }
        } else {
          result[resultIndex] = (byte) s.charAt(i);
          resultIndex++;
        }
      }
      return new String(result, 0, resultIndex);
    }
  }


```
