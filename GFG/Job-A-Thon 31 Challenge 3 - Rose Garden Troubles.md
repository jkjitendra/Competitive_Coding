# Rose Garden Troubles

## Problem Statement:


Geek, a devoted boyfriend, wants to surprise his girlfriend Geekina with a beautiful bouquet of roses. Geek has a **rose garden with N roses**, each of which has a certain **value** associated with it. However, Geek faces a unique challenge in choosing the roses for the bouquet. He must select a **consecutive sequence of roses** in such a way that the **greatest common divisor (GCD)** of the values of all the chosen roses is **less than or equal to a given number, K.**

Geek seeks your help in finding the number of ways he can create the bouquet while adhering to this GCD constraint. Can you help him find the solution?

#### Example 1:

```
Input:

N = 4
K = 3
arr = [4, 8, 5, 11]

Output:
5

Explanation:
The subarrays (bouquets) satisfying the gcd constraint are [4,8,5], [4,8,5,11], [8.5.11]. [5.11]. [8.5].
```

#### Example 2:

```
Input:
N = 5
K = 3
arr = [8, 14, 16, 36, 40]

Output:
7

Explanation:
The subarrays that satisfy the constraint are [8, 14], [8, 14, 16], [8, 14, 16, 36], [8, 14, 16, 36, 40], [14, 16], [14, 16, 36], [14, 16, 36, 40].
```

#### Example 3:

```
Input:
N = 20
K = 1
arr = [30, 94, 19, 12, 83, 35, 8, 31, 92, 56, 42, 50, 43, 37, 40, 96, 33, 39, 2, 24]

Output:
178

Explanation:
The subarrays that satisfy the constraint are 
```

#### Your Task:
This is a function problem. The input is already taken care of by the driver code. You only need to complete the function CountBouquets() that takes a number of flowers (N), value of each flower (arr[]) and the integer K as input arguments. Return an integer denoting the number of subarrays satisfying the condition. The driver code takes care of the printing.

#### Constraints:

- 1 <= n <= 10<sup>5</sup>
- 1 <= k <= 10<sup>9</sup>
- 1 <= arr[i] <= 10<sup>9</sup>

## Solution:

#### Method 1:

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int t = sc.nextInt();
        while(t-- > 0) {
            long n = sc.nextLong();
            long k = sc.nextLong();
            ArrayList<Long> arr = new ArrayList<>();
            for (int i = 0; i < n; i++) {
                arr.add(sc.nextLong());
            }
            Solution obj = new Solution();
            System.out.println(obj.score(n, k));
        }
        sc.close();
    }
}

class Solution {
    public long CountBouquets(long n, long k, ArrayList<Long> arr) {
        // code here
        long count = 0;
        for (int start = 0; start < n; start++) {
            long currentGCD = arr.get(start);
            for (int end = start; end < n; end++) {
                currentGCD = gcd(currentGCD, arr.get(end));
                if (currentGCD <= k) {
                    // Directly add to count and break to avoid extra iterations.
                    count += (n - end);
                    break;
                }
                // Once the GCD is greater than k, further extending the window is not useful.
            }
            // Optimization: Pre-emptively break if the single element's GCD is already greater than k.
            if (currentGCD > k) {
                break;
            }
        }
        return count;
    }
    
    private long gcd(long a, long b) {
        while (b != 0) {
            long temp = b;
            b = a % b;
            a = temp;
        }
        return a;
    }
}
```
