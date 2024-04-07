# Maximize the Minimum Importance

## Problem Statement:

You are given an integer array named `arr` with a size of `n` and two integers, `r` and `k`.

You are allowed to perform the following operation  **at most `k` times** : Select any index `i`, where `0 <= i < n`, and increase the value of `arr[i]` by 1.

After performing up to `k` operations, your goal is to determine the **maximum possible minimum importance** of an element in the array. The **importance** of an element at index `i` in the array is calculated as the **sum of all elements** in the range `[max(0, i - r), min(i + r, n - 1)]`.

**Example 1:**

**Input:** <br/>
n = 5 <br/>
r = 1 <br/>
k = 2 <br/>
arr = [1, 2, 4, 5, 0] <br/>

**Output:** 5 <br/>

**Explanation:** <br/>
One of the optimal ways is to perform all 2 operations at index 1.<br/>
So, arr will become [1, 4, 4, 5, 0].
 - Importance of element at index 0 = 1 + 4 = 5.
 - Importance of element at index 1 = 1 + 4 + 4 = 9.
 - Importance of element at index 2 = 4 + 4 + 5 = 13.
 - Importance of element at index 3 = 4 + 5 + 0 = 9.
 - Importance of element at index 4 = 5 + 0 = 9.

So the minimum importance of an element is 5. Since it is not possible to obtain a larger importance, we return 5.

**Example 2:**

**Input:** <br/>
n = 4 <br/>
r = 0 <br/>
k = 3 <br/>
arr = [4, 4, 4, 4] <br/>

**Output:** 4  <br/>

**Explanation:** <br/>
It can be proved that we cannot make the minimum importance of an element greater than 4.

**Your Task:**

You have to complete the function `maxMinImportance()` which takes 3 integers `n`, `r`, `k`, and an integer array `arr`. It should return an integer denoting the maximum possible minimum importance of an element in the array.

**Constraints:**

- `1 <= n <= 10^5`
- `1 <= arr[i] <= 10^5`
- `0 <= r <= n - 1`
- `0 <= k <= 10^9`


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
            
            int r;
            r = Integer.parseInt(br.readLine());
            
            int k;
            k = Integer.parseInt(br.readLine());
            
            int[] arr = IntArray.input(br, n);
            
            Solution obj = new Solution();
            int res = obj.maxMinImportance(n, r, k, arr);
            
            System.out.println(res);
        }
    }
}

class Solution {
    public static int maxMinImportance(int n, int r, int k, int[] arr) {
        long ans = 0L;
        long low = 0L;
        long high = (long)1e15;
    
        while (low <= high) {
            long mid = (high + low) / 2L;
            if (check(mid, arr, r, k)) {
                ans = mid;
                low = mid + 1;
            } else {
                high = mid - 1;
            }
        }
        return (int) ans;
    }

    private static boolean check(long imp, int[] arr1, int r, int k) {
        long window = 0;
        int[] arr = arr1.clone();
        int n = arr.length;
    
        for (int i = 0; i < n; i++) {
            if (i == 0) {
                for (int j = 0; j <= r && j < n; j++) {
                    window += arr[j];
                }
            } else {
                if (i + r < n) {
                    window += arr[i + r];
                }
                if (i - r - 1 >= 0) {
                    window -= arr[i - r - 1];
                }
            }
        
            if (window >= imp) {
                continue;
            }
        
            if (window + k >= imp) {
                int updateIndex = Math.min(i + r, n - 1);
                arr[updateIndex] += imp - window;
                k -= imp - window;
                window += imp - window;
            } else {
                return false;
            }
        }
        return true;
    }
}

```
