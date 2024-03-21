# It's PayDay

## Problem Statement:

Geek **borrowed money** from two people A and B. He borrowed amount X1 from A at an **interest rate of R1%** and amount X2 from B at an **interest rate of R2%**. As exactly one year has passed since he borrowed the money. Geek needs to return the money back to A and B.

Can you help Geek find out to whom he owes more amount of interest money (that is the extra amount of money Geek needs to pay apart from the borrowed amount)?

If he owes both of them the same amount of interest, return "EQUAL".

#### Example 1:

```
Input:
X1 = 100
R1 = 5
X2 = 50
R2 = 10

Output:
EQUAL

Explanation:
Geek owes 5% of Rs 100 which is Rs 5 as interest money to A, and the same amount to B (10% os Rs 50).
```

#### Example 2:

```
Input:
X1 = 1000
R1 = 50
X2 = 200
R2 = 20

Output:
A

Explanation:
Geek owes 50% of Rs 1000 which is Rs 500 as interest money to A, and 20% of Rs 200 which is Rs 40 to B. Since 500 > 40 therefore output is A.
```

#### Your Task:
This is a function problem. The input is already taken care of by the driver code. You only need to complete the function PayDay() that takes four integers x1, r1, x2, r2 as input arguments. Return a string denoting the person to whom Geek owes more money. The driver code takes care of the printing.

#### Constraints:
- 1 <= X1, X2 <= 10<sup>9</sup>
- 1 <= R1, R2 <= 99

## Solution:

#### Method 1:

```java
import java.io;
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();
        while(t-- > 0) {
            int x1 = sc.nextInt();
            int r1 = sc.nextInt();
            int x2 = sc.nextInt();
            int r2 = sc.nextInt();
            
            Solution obj = new Solution();
            System.out.println(obj.PayDay(x1, r1, x2, r2));
        }
        sc.close();
    }
}

class Solution {
    public String PayDay(int x1, int r1, int x2, int r2) {
        double interestToA = x1 * (r1/100.0);
        double interestToB = x2 * (r2/100.0);

        if (interestToA > interestToB) {
            return "A";
        } else if (interestToA < interestToB) {
            return "B";
        } else {
            return "EQUAL";
        }
    }
}
```
