# PalindromeDivisionChecker

## Problem Statement

You are given a range of integers from startRange to endRange (inclusive) and a specific divisor. Your task is to find all numbers within this range such that when the number is divided by the given divisor, the quotient is also a palindrome. Write a program that finds these numbers within the given range. A number is considered valid if both the number and the quotient are palindromes and the number is divisible by the given divisor without leaving a remainder.

**Input:**
- The input consists of three integers: startRange, endRange, and divisor.

**Output:**
- Pairs of numbers within the given range where the number divided by the divisor results in a palindromic quotient. For each pair, include the quotient.
- If there are no such pairs, the program should indicate that no matching pairs were found by printing “No matching pairs found”.

**Example 1:**<br />
```
Input:

startRange = 1
endRange = 200
divisor = 11

Output:

Number: 121, Divisor: 11, Quotient: 11

Explanation:

Number 121 is a palindrome and 121 divided by 11 is 11, which is also a palindrome. Therefore, (121, 11) is a valid pair.
```

**Example 2:**<br />
```
Input:

startRange = 1
endRange = 100
divisor = 7

Output:

No matching pairs found.

Explanation:

There don't exist any pairs whose quotient is a palindrome in the given range.
```

**Constraints:**<br/>
- 1 <= startRange <= endRange <= 10^6
- 1 <= divisor <= 10^6

## Solution

#### Method 1:

```java
import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class PalindromeDivisionChecker {

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int startRange = sc.nextInt();
        int endRange = sc.nextInt();
        int divisor = sc.nextInt();
        sc.close();

        List<String> results = findPalindromePairs(startRange, endRange, divisor);
        if (results.isEmpty()) {
            System.out.println("No matching pairs found.");
        } else {
            for (String result : results) {
                System.out.println(result);
            }
        }
    }

    private static List<String> findPalindromePairs(int start, int end, int divisor) {
        List<String> pairs = new ArrayList<>();

        for (int num = start; num <= end; num++) {
            if (isPalindrome(num)) {
                if (num % divisor == 0) {
                    int quotient = num / divisor;
                    if (isPalindrome(quotient) && num != divisor) {
                        pairs.add("Number: " + num + ", Divisor: " + divisor + ", Quotient: " + quotient);
                    }
                }
            }
        }
        return pairs;
    }

    private static boolean isPalindrome(int num) {
        String str = String.valueOf(num);
        return str.equals(new StringBuilder(str).reverse().toString());
    }
}
```