# Prefix Distinct

## Problem Statement:

Given an integer array **arr[]** of size  **n** . Your task is to return an **array answer of size n** such that **answer[i]** represents the number of distinct elements in the prefix of the arr till **i <sup>th </sup>** index (0<=i<=n-1).

**Example 1:**

**Input:**<br/>
n=3<br/>
arr={1,2,1}<br/>

**Output:**<br/>
{1,2,2}

**Explanation:**<br/>
The number of distinct elements in prefix of
arr upto index 0 is 1 {1}.<br/>
The number of distinct elements in prefix of
arr upto index 1 is 2 {1,2}.<br/>
The number of distinct elements in prefix of arr
upto index 2 is 2 {1,2} (as arr[2] is same as arr[0]
so counted only once).

**Example 2:**

**Input:**<br/>
n=4<br/>
arr={1,1,1,2}<br/>

**Output:**<br/>
{1,1,1,2}

**Explanation:**<br/>
The number of distinct elements in prefix
upto index 2 is 1{1} and for index 3 we have
two distinct values{1,2}.

**Your Task:**<br/>
You don't need to read input or print anything. Your task is to complete the function **prefixDistinct()** which takes an integer **n** and an integer array **arr[]** as input parameters and return an array answer of size n such that answer[i] represents the number of distinct elements in the prefix of the arr till ith index.

**Constraints:**
 - 2 <= **n** <= 10 <sup>5</sup>
 - 1 <= **arr[i]** <= 10 <sup>9</sup>

## Solution:

##### Method 1:

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        PrintWriter ot = new PrintWriter(System.out);
        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            int n = Integer.parseInt(br.readLine().trim());
            String s[] = br.readLine().trim().split(" ");
            int arr[] = new int[n];

            for (int i = 0; i < n; i++) {
                arr[i] = Integer.parseInt(s[i]);
            }

            Solution obj = new Solution();
            int ans[] = obj.prefixDistinct(n, arr);
            for (int x: ans) {
                ot.print(x + " ");
            }
            ot.println();
        }
        ot.close();
    }
}

class Solution {
    public int[] prefixDistinct(int n, int[] arr) {
        int[] answer = new int[n];
        Set<Integer> distinctElements = new HashSet<>();
        for (int i = 0; i < n; i++) {
            distinctElements.add(arr[i]);
            answer[i] = distinctElements.size();
        }
        return answer;
    }
}    
```