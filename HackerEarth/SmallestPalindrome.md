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
1 <= T <= 10
1 <= N <= 10^5

**Sample Input**
2
3
4

**Sample Output**
161
1001

**Explanation**
***The first test case***
Given N = 3
Approach
- 161 is the smallest 3-digit number that is palindrome and divisible by 7. Thus, it is the answer.

## Solution

#### Method1:

```java
import java.io.*;
import java.util.*;

public class TestClass {
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamRead(System.in));
        PrintWriter wr = new PrintWriter(System.out);
        int T = Integer.parseInt(br.readLine().trim());
        for (int t_i = 0; t_i < T; i++) {
            int N = Integer.parseInt(br.readLine().trim());
            String out_ = solve(N);
            System.out.println(out_);
        }
        wr.close();
        br.close();
    }

    static String solve(int N) {
        long start = (long) Math.pow(10, (N - 1) / 2);
        long end = (long) Math.pow(10, (N + 1) / 2);
        
        for (long i = start; i < end; i++) {
            String str = Long.toString(i);
            String reverseStr = new StringBuilder(str).reverse().toString();
            long palindrome;
            if (N % 2 == 0) {
                palindrome = Long.parseLong(str + reverseStr);
            } else {
                palindrome = Long.parseLong(str + reverseStr.substring(1));
            }
            
            if (palindrome >= Math.pow(10, N - 1) && palindrome < Math.pow(10, N) && palindrome % 7 == 0) {
                return String.valueOf(palindrome);
            }
        }
        return "";
    }
}
```;