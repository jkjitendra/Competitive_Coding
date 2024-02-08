# Letter Combinations of a Phone Number

## Problem Statement:

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent. Return the answer in  **any order** .

A mapping of digits to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

![](https://assets.leetcode.com/uploads/2022/03/15/1200px-telephone-keypad2svg.png)

**Example 1:**

<pre><strong>Input:</strong> digits = "23"
<strong>Output:</strong> ["ad","ae","af","bd","be","bf","cd","ce","cf"]
</pre>

**Example 2:**

<pre><strong>Input:</strong> digits = ""
<strong>Output:</strong> []
</pre>

**Example 3:**

<pre><strong>Input:</strong> digits = "2"
<strong>Output:</strong> ["a","b","c"]
</pre>

**Constraints:**

* `0 <= digits.length <= 4`
* `digits[i]` is a digit in the range `['2', '9']`.


## Solution:

#### Method 1:

```java
class Solution {
  public List<String> letterCombinations(String digits) {
    List<String> result = new ArrayList<>();
    if (digits == null || digits.length() == 0) {
      return result;
    }

    Map<Character, String> phoneMap = new HashMap<>();
    phoneMap.put('2', "abc");
    phoneMap.put('3', "def");
    phoneMap.put('4', "ghi");
    phoneMap.put('5', "jkl");
    phoneMap.put('6', "mno");
    phoneMap.put('7', "pqrs");
    phoneMap.put('8', "tuv");
    phoneMap.put('9', "wxyz");
  
    StringBuilder combination = new StringBuilder();
    backtrack(result, phoneMap, digits, 0, combination);
    return result;
  }
  
  private void backtrack(List<String> result, Map<Character, String> phoneMap, String digits, int index, StringBuilder combination) {
    if (index == digits.length()) {
      result.add(combination.toString());
      return;
    }
  
    char digit = digits.charAt(index);
    String letters = phoneMap.get(digit);
    for (int i = 0; i < letters.length(); i++) {
      combination.append(letters.charAt(i));
      backtrack(result, phoneMap, digits, index + 1, combination);
      combination.deleteCharAt(combination.length() - 1);
    }
  }
}
```
