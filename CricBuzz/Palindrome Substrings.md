# Palindrome Substrings

## Problem Statement

For a string *s* and an integer *k*, a selection of substrings is valid if the following conditions are met:

- The length of every substring is greater than or equal to k
- Each substring is a palindrome.
- No two substrings overlap.

Determine the maximum number of valid substrings that can be formed from *s*.

**Notes:**

- A substring is a group of adjacent characters in a string.
- A **palindrome** is a string that reads the same backward as forward.

**Example:**

s = "aababaabce"

k = 3

a **ababa** abce

a **aba** **baab** ce

Any valid substring must be k or more characters long. Either 1 or 2 non-overlapping palindromes can be formed. Return 2, the maximum number that can be formed.

**Function Description: **
Complete the function *getMaxSubstrings* in the editor below.

*getMaxSubstrings* has the following parameters:

*string s*: the given string
*int k*: the minimum length of a valid substring

**Returns:**

*int:* the maximum number of valid substrings that can be formed

**Constraints**

• 1 ≤ |s| ≤ 2.10^3

• 1 ≤ k ≤ |s|

**Input Format For Custom Testing:**

The first line contains the string *s.*
The next line contains an integer, *k.*

**Sample Case 0:**
    **Sample Input For Custom Testing**

```
STDIN                FUNCTION
------		         ---------
ababaeocco   ->      s = "ababaeocco"
4            ->      k = 4
```

**Sample Output:**

2

**Explanation:**

**ababa** e **occo**

The bold substrings are palindromes with k = 4 characters or more.(**ababa** and **occo**)

**Sample Case 1:**
    **Sample Input For Custom Testing**

```
STDIN                FUNCTION
------		         ---------
aaaaabb      ->      s = "aaaaabb"
2            ->      k = 2
```

**Sample Output:**

3

**Explanation:**

**aa aa** a **bb**

This is one maximal solution. The substrings can match as long as they do not overlap.(aa(1st pair), aa(2nd pair), and bb).

## Solution

#### Method 1:

```java
import java.io.*;
import java.math.*;
import java. security.*;
import java.text.*; import java.util.*;
import java.util.concurrent.*;
import java.util. function.*; import java.util.regex.*;
import java.util.stream. *;
import static java.util.stream.Collectors.joining; import static java.util.stream.Collectors.toList;

class Result {

    public static int getMaxSubstrings(String s, int k) {
        int n = s.length();
        List<int[]> palindromes = new ArrayList<>();

        // Find all palindromes of length >= k
        for (int start = 0; start <= n - k; start++) {
            for (int end = start + k - 1; end < n; end++) {
                if (isPalindrome(s, start, end)) {
                    palindromes.add(new int[]{start, end});
                }
            }
        }

        // Sort palindromes by their ending index to ensure we can find the maximum number of non-overlapping palindromes
        Collections.sort(palindromes, (a, b) -> a[1] - b[1]);

        int count = 0;
        int lastEnd = -1;

        // Select non-overlapping palindromes
        for (int[] p : palindromes) {
            if (p[0] > lastEnd) {
                count++;
                lastEnd = p[1];
            }
        }

        return count;
    }
  
    private static boolean isPalindrome(String str, int start, int end) {
        while (start < end) {
            if (str.charAt(start) != str.charAt(end)) {
                return false;
            }
            start++;
            end--;
        }
        return true;
    }
}

public class Solution{
    public static void main(String[] args) {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BUfferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));
        String s = bufferedReader.readLine();
        String k = bufferedReader.readLine();
        String result = Result.getMaxSubstrings(s, k);
        bufferedWriter.write(result);
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}
```
