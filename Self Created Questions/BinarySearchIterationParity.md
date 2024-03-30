# Binary Search Iteration Parity

## Problem Statement:

You are given a range of integers from **startRange** to **endRange** (inclusive). Your task is to find all the numbers within this range such that the number and its reverse have the same number of iterations to be found using binary search. Additionally, filter out the numbers whose reverse is the same as the number itself. Write a program that finds pairs of numbers within a given range, where each number and its reverse undergo binary search within the same range, and the number of iterations required to find each in the binary search process is the same. It's important to note that a number and its reverse are considered a valid pair only if they are not identical (i.e., the reverse of 121 is 121, so it's not considered, but the reverse of 12 is 21, which is considered).

**Input:**

* The input consists of two integers **startRange** and  **endRange** , representing the range of integers.

**Output:**

* Pairs of numbers within the given range where each number and its reverse have the same number of iterations required in a binary search process. For each pair, also include the shared iteration count.
  If there are no such pairs, the program should indicate that no matching pairs were found by printing "No matching pairs found".

**Example1:**

```
Input:

startRange = 1
endRange = 100

Output:

Number: 10, Reverse: 1,  Iterations: 6
Number: 18, Reverse: 81, Iterations: 4
Number: 20, Reverse: 2,  Iterations: 7
Number: 23, Reverse: 32, Iterations: 6
Number: 24, Reverse: 42, Iterations: 7
Number: 27, Reverse: 72, Iterations: 7
Number: 29, Reverse: 92, Iterations: 6
Number: 32, Reverse: 23, Iterations: 6
Number: 39, Reverse: 93, Iterations: 7
Number: 42, Reverse: 24, Iterations: 7
Number: 47, Reverse: 74, Iterations: 7
Number: 58, Reverse: 85, Iterations: 7
Number: 72, Reverse: 27, Iterations: 7
Number: 74, Reverse: 47, Iterations: 7
Number: 80, Reverse: 8,  Iterations: 7
Number: 81, Reverse: 18, Iterations: 4
Number: 85, Reverse: 58, Iterations: 7
Number: 92, Reverse: 29, Iterations: 6
Number: 93, Reverse: 39, Iterations: 7

Explanation:

Number 10 can be found in 6 iterations using binary search in the range 1 to 100. Similarly reverse of number 10 i.e., number 1 can also be found in 6 iterations in the range 1 to 100. Therefore, 10 and its reverse are a valid pair for the given range of integers.
```

**Example2:**

```
Input:

startRange = 1
endRange = 10

Output:

No matching pairs found.

Explanation:

There doesn't exists any pair whose iterations are equal in the given range.
```


**Constraints:**

* 1 <= startRange <= endRange <= 10^6
* The search range for binary search is always from `start` to `end`.

## Solution:

#### Method 1:

```java
package org.program;

import java.util.ArrayList;
import java.util.List;
import java.util.Scanner;

public class BinarySearchIterationParity {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int startRange = sc.nextInt();
        int endRange = sc.nextInt();
        sc.close();

        List<String> results = findNumbersWithSameIterations(startRange, endRange);
        if (results.isEmpty()) {
            System.out.println("No matching pairs found.");
        } else {
            for (String result : results) {
                System.out.println(result);
            }
        }
    }

    public static List<String> findNumbersWithSameIterations(int start, int end) {
        List<String> matches = new ArrayList<>();
        for (int num = start; num <= end; num++) {
            int iterations = 0;
            int reverseIterations = 0;
            int reverse = reverseNumber(num);
            if (num != reverse) {
                iterations = binarySearchIterations(num, start, end);
                reverseIterations = binarySearchIterations(reverse, start, end);
            }

            if (iterations != -1 && iterations != 0 && iterations == reverseIterations) {
                matches.add("Number: " + num + ", Reverse: " + reverse + ", Iterations: " + iterations);
            }
        }
        return matches;
    }

    public static int binarySearchIterations(int target, int start, int end) {
        int iterations = 0;
        int left = start;
        int right = end;

        while (left <= right) {
            iterations++;
            int mid = left + (right - left) / 2;

            if (mid == target) {
                return iterations;
            } else if (mid < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return -1;
    }

    public static int reverseNumber(int num) {
        int reversed = 0;
        while (num != 0) {
            int digit = num % 10;
            reversed = reversed * 10 + digit;
            num /= 10;
        }
        return reversed;
    }
}
```