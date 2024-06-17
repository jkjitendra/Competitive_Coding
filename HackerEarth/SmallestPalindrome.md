# Smallest Palindrome

## Problem Statement

Given an integer N, fibd the smallest palindromic number of N digits that is divisible by 7. A plaindromic number is one which remains the same when its digits are reversed.

**Function description:**
Complete the function **solve**. This function takes the following parameter and returns the required answer:

- N: Represents the number of required digits in the palindrome.

**Input format for custom testing:**
**Note:** Use this input format if you are testing against custom input or writing code in a language where we don't provide boilerplate code.

- The first line contains T, which represents the number of test cases.
- For each test case:
  - The first line contains a single integer N denoting the value of N.

**Output format:**
Print a single line containing the answer.

**Constraints:**

- 1 <= T <= 10
- 1 <= N <= 10^5

**Sample Input**<br/>
2<br/>
3<br/>
4<br/>

**Sample Output**<br/>
161 <br/>
1001

**Explanation**<br/>
***The first test case***<br/>
Given N = 3<br/>
Approach<br/>

- 161 is the smallest 3-digit number that is palindrome and divisible by 7. Thus, it is the answer.

## Solution

#### Method 1:

```java
import java.io.*;
import java.util.*;
import java.math.BigInteger;

public class TestClass {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        PrintWriter wr = new PrintWriter(System.out);
        int T = Integer.parseInt(br.readLine().trim());
        for (int t_i = 0; t_i < T; t_i++) {
            int N = Integer.parseInt(br.readLine().trim());
            String out_ = solve(N);
            System.out.println(out_);
        }
        wr.close();
        br.close();
    }

    private static String solve(int N) {
        if (N == 1) return "7";
        if (N == 2) return "77";

        // Start creating palindromes from the smallest number with N/2 or (N/2 + 1) digits, filled with zero in between
        BigInteger start = BigInteger.TEN.pow((N - 1) / 2);  // 10^((N-1)/2)
        BigInteger end = BigInteger.TEN.pow((N + 1) / 2);  // 10^((N+1)/2), exclusive
        BigInteger seven = BigInteger.valueOf(7);

        for (BigInteger num = start; num.compareTo(end) < 0; num = num.add(BigInteger.ONE)) {
            String smallestPalindrome = formPalindrome(num.toString(), N);
            BigInteger palNum = new BigInteger(smallestPalindrome);
            if (palNum.mod(seven).equals(BigInteger.ZERO)) {
                return palNum.toString();
            }
        }

        return ""; // In case no valid palindrome is found
    }

    private static String formPalindrome(String half, int N) {
        StringBuilder sb = new StringBuilder(half);
        StringBuilder reverse = new StringBuilder(half);
        if (N % 2 == 1) { // If N is odd, skip the last digit in the reversed part
            reverse.reverse().deleteCharAt(0);
        } else { // If N is even, just reverse
            reverse.reverse();
        }
        return sb.append(reverse).toString();
    }
}
```
