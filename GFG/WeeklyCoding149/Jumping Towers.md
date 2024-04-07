# Jumping Towers

## Problem Statement:

Given **n towers** of  **varying heights** , Geek stands at the  **top of the first tower** . In one jump, Geek can perform **exactly one** of the following actions:

1. If Geek is currently at the i-th tower, he can  **jump to the i+1-th tower** .
2. Geek can jump to  **any other tower j** , such that  **height[i] is same as height[j]** .

Note: Geek can perform the  **2nd action at most once** .

Find the **minimum number of jumps** required by Geek to reach the last tower.

**Example 1:**

**Input:**<br/>
n = 5<br/>
heights = [1, 2, 1, 3, 2]<br/>

**Output:**<br/>
2

**Explanation:**<br/>
After the first jump Geek, will reach the 2nd tower. In the next jump, he can directly jump to the last tower as they have the same height of 2.

**Example 2:**

**Input:**<br/>
n = 6<br/>
heights = [1, 2, 3, 3, 2, 4]<br/>

**Output:**<br/>
3

**Explanation:**<br/>
After the first jump Geek, will reach the 2nd tower. In the next jump, he can directly jump to the fifth tower as they have the same height of 2. In the 3rd jump, he will jump to the last tower.

**Your Task:**<br/>
This is a function problem. The input is already taken care of by the driver code. You only need to complete the function minJumps() that takes an integer n and an integer array denoting heights as input arguments. Return an integer denoting the minimum number of jumps. The driver code takes care of the printing.

**Constraints:**
 - 1 <= n <= 10^5
 - 1 <= heights[i] <= 10^9


## Solution:

#### Method 1:

```java
import java.io.*;
import java.util.*;

class IntArray {
    public static int[] input(BufferedReader br, int n) throws IOException {
        String[] s = br.readLine().trim().split(" ");
        int[] a = new int[n];
        for (int i = 0; i < n; i++) {
            a[i] = Integer.parseInt(s[i]);
        }
        return a;
    }

    public static void print(int[] a) {
        for (int e : a) {
            System.out.print(e + " ");
        }
        System.out.println();
    }

    public static void print(ArrayList<Integer> a) {
        for (int e : a) {
            System.out.print(e + " ");
        }
        System.out.println();
    }
}

class GFG {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t;
        t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            int n;
            n = Integer.parseInt(br.readLine());
  
            int[] arr = IntArray.input(br, n);
  
            Solution obj = new Solution();
            int res = obj.maxMinImportance(n, arr);
  
            System.out.println(res);
        }
    }
}

class Solution {
    public static int minJumps(int n, int[] arr) {
        int minNoOfJumps = n-1;
        HashMap<Integer, Integer> height = new HashMap<>();
        for (int i = n-1; i >= 0; i--) {
            if (height.containsKey(arr[i)) {
		minNoOfJumps = Math.min(minNoOfJumps, n - (height.get(arr[i]) - i));
            } else {
		height.put(arr[i], i);
            }
        }
	return minNoOfJumps;
    }
}
```
