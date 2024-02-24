# Maximize the Fuel

## Problem Statement:

Consider a car with a maximum fuel capacity of **n** litres. Two infinite-capacity containers are available, one containing **petrol** and the other containing **diesel**. Each move allows you to transfer **a** litre petrol from the petrol container or **b** litre of diesel from the diesel container into the car.

The task is to **maximize** the total fuel in the car, subject to the following **conditions**:

- The total fuel in the car cannot exceed **n** litre.
- Either **a** litre of petrol or **b** litre of diesel can be added in **one** move
- The current fuel level of the car can be decreased by **half**(round down in case of float values) at most **once**.

The goal is to formulate an approach that determines the **maximum** achievable fuel amount in the car.

**Exmaple 1:**

```
Input:
n=8
a=5
b=6
Output:
8
Explanation:
In the first move, put b=6 litres of diesel and the current fuel is of 6 litres.
Half the current fuel volume, so the current fuel volume is of 3 litres.
In the second move, put a=5 litres of petrol and the current fuel is of 8 litres.
Now, the current fuel capacity can't be exceeded more than the maximum fuel capacity. So, the answer to this test case is 8.
```

**Example 2:**

```
Input:
n=8
a=6
b=6
Output:
6
Explanation:
In the first move, put b=6 litres of diesel and the current fuel is of 6 litres.
It can be proven that the fuel capacity can't exceed 6 litres.
```

**Your Task:**

You don't need to read or print anything. Your task is to complete the function **maximizeTheFuel()** which takes three integers **n, a and b** as input parameters and returns an integer representing the **maximum amount of fuel that can be placed in the car.**

**Constraints:**

- 1 <= n <= 10<sup>9</sup>
- 1 <= n/max(a,b) <= 10<sup>6</sup>
- 1 <= a,b <= n

## Solution:

#### Method 1:

```java
import java.io.*;
import java.util.*;

public class GFG {
    public static void main(String args[]) {
        Scanner sc=new Scanner(System.in);
        int t=sc.nextInt();
        while(t-->0)
        {
            int a=sc.nextInt();
            int b=sc.nextInt();
            int c=sc.nextInt();
            Solution obj=new Solution();
            System.out.println(obj.maximizeTheFuel(a,b,c));
        }
    }
}

class Solution 
{
    private int fun(int c, int a, int b) {
        int ans = 0;
        if (b > a) {
            int temp = a;
            a = b;
            b = temp;
        }
        for (int i = 0; i <= c / a; i++) {
            ans = Math.max(ans, a * i + ((c - a * i) / b) * b);
            if (ans == c)
                break;
        }
        return ans;
    }


    public int maximizeTheFuel(int n, int a, int b) 
    {
        int res = 0;
        int nab, na2b, nab2, na2b2;
        if (a + b <= n) {
            nab = fun(n, a, b);
            na2b = a / 2 + fun(n - a / 2, a, b);
            nab2 = b / 2 + fun(n - b / 2, a, b);
            na2b2 = (a + b) / 2 + fun(n - (a + b) / 2, a, b);
            res = Math.max(Math.max(nab, na2b), Math.max(nab2, na2b2));
        } else {
            nab = fun(n, a, b);
            na2b = a / 2 + fun(n - a / 2, a, b);
            nab2 = b / 2 + fun(n - b / 2, a, b);
            res = Math.max(nab, Math.max(na2b, nab2));
        }
        return res;
    }
}

```