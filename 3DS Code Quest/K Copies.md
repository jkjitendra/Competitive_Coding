# K Copies

## Problem Statement:

You are given a string *S*. You have to create *K* copies of this string and concatenate all these copies to the original string.
Concatenation is done like this:

- For a given copy, *i*, **1<=i<=k**, if *i* is odd, reverse the given string and concatenate, else concatenate the original string.

**Input Format**

- The first line contains a string *S*.
- The next line contains an integer *K*.

**Constraints**

- 1<=|S|<=1000
- 1<=K<=1000
- All the characters are lowercase English letters.

**Output Format**

- Output the resultant string

**Sample Test Case**

Sample Input
```
abc
2
```

Sample Output
```
abccbaabc
```

Explanation

You have to concatenate 2 copies of the original string in the given string. The 1<sup>st</sup> copy string will be **cba** and the 2<sup>nd</sup> copy will be **abc**, so the final string after concatenation will be **abccbaabc**.

## Solution:

#### Method 1:
```java
class Result {
    public static String solve(String S, int K) {
        StringBuilder sb = new StringBuilder(S);
        for (int i = 1; i <= K; i++) {
            if (i%2 == 1) {
                sb.append(new StringBuilder(S).reverse().toString());
            } else {
                sb.append(S);
            }
        }
        return sb.toString();
    }
}
```