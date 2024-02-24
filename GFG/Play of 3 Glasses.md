# Play of 3 Glasses

## Problem Statement:

There are three glasses of water labeled as **a, b, c** each with varying capacities and the ability to contain different volumes of water.

Let **(c1, w1)** be the capicity and the current volume of water in glass **a**, respectively, **(c2, w2)** be the capacity and the current volume of water in glass **b**, respectively and **(c3, w3)** be the capacity and the current volume of water in glass **c**, respectively.

The task is to sequentially pour water from glas **a** to glass **b**, then from **b to c**, followed by **c to a**, and so on in a cyclical fashion, repeating this process for a total of **10<sup>5</sup> operations**. It is important to note that when transferring water from glass **a** to **b**, the pouring continues until either glass **a** is emptied or glass **b** is filled.

Given this pattern, determine the final amounts of water in each glass after completing the 10<sup>5</sup> pour operations. Specifically, identify the quantity of water present in each glass, taking into account the constraints and cyclic nature of the pouring sequence.

Note- Please go through the example for better understanding of the process.

```
Example 1:

Input:
Capacity of glass a is 10 units and the water in it is 3 units.
Capacity of glass b is 11 units and the water in it is 4 units.
Capacity of glass c is 12 units and the water in it is 5 units.

Output:
0 10 2

Explanation:
The water in each glass is as follows:

Initial State: 3   4   5
1. Pour a->b:  0   7   5
2. Pour b->c:  0   0   12
3. Pour c->a:  10  0   12
4. Pour a->b:  0   10  2 
5. Pour b->c:  0   0   12
and so on...
It can be proved that the final configuration would be [0, 10, 2].
```

**Your Task:**

You don't need to read input or print anything. Your task is to complete the function **playOfGlasses()** which takes 6 integers c1, w1, c2, w2, c3, w3 as input parameters and return an integer vector of size 3, which represents the configuration of volumes of water in all the 3 glasses after performing all operations, as, the first interger the volume of water in glass **a**, second integer denotes the volume of water in glass **b**, and the third integer denotes the volume of water in glass **c**.

**Constraints:**

1<=c1,w1,c2,w2,c3,w3<=10<sup>4</sup>

## Solution:

#### Method 1:

```java
import java.io.*;
import java.util.*;

public class GFG {
    public static void main(String args[]) 
    {
        Scanner sc=new Scanner(System.in);
        int t=sc.nextInt();
        while(t-- > 0)
        {
            int c1=sc.nextInt();
            int w1=sc.nextInt();
            int c2=sc.nextInt();
            int w2=sc.nextInt();
            int c3=sc.nextInt();
            int w3=sc.nextInt();
            Solution s=new Solution();
            ArrayList<Integer> res=s.playOfGlasses(c1,w1,c2,w2,c3,w3);
            for(int i=0;i<res.size();i++)
            {
                System.out.print(res.get(i)+" ");
            }
            System.out.println("");
        }
    }
}

class Solution{
    private static final int MAX_ITERATIONS = 100000;
    ArrayList<Integer> playOfGlasses(int c1,int w1,int c2,int w2,int c3,int w3)
    {
        int temp;
        for (int i = 0; i < MAX_ITERATIONS; i++) {
            if (i%3 == 0) {
                temp = Math.min(w1, c2-w2);
                w1 -= temp;
                w2 += temp;
            } else if (i%3 == 1) {
                temp = Math.min(w2, c3-w3);
                w2 -= temp;
                w3 += temp;
            } else {
                temp = Math.min(w3, c1-w1);
                w3 -= temp;
                w1 += temp;
            }
        }
        return new ArrayList<>(Arrays.asList(w1, w2, w3));
    }
}
```