# Beautiful Cities - I

## Problem Statement:

There are **n** cities in a Geekland. Each city is given some **beautifulness** by the king. Cities with **different** beautifulness don't like to trade with each other. You are given with **q** **queries** each consisting of two integers **u** and  **v** . You need to tell if all the cities from u to v (both inclusive) can trade with every other city from u to v.

**Example 1:**

**Input:**<br/>
n = 8<br/>
beautifulness = {2,2,2,2,1,1,1,3}<br/>
q = 5<br/>
queries = {{1,4},{2,5},{5,7},{1,8},{6,6}}<br/>

**Output:**<br/>
{1,0,1,0,1}

**Explanation:**<br/>
All the cities from 1 to 4 have a beautifulness of 2 therefore any city can trade with any other city. So the answer for the first query is 1.
City 5 does not trade with city 2,3 and 4. So the answer for the second query is 0.
Similarly, for other queries.

**Example 2:**

**Input:**<br/>
n = 6<br/>
beautifulness = {2,1,6,5,3,4}<br/>
q = 4<br/>
queries = {{1,2},{2,5},{5,6},{6,6}}<br/>

**Output:**<br/>
{0,0,0,1}

**Explanation:**<br/>
None of the queries except the last one has all cities which can trade with each other.

**Your task:**

You don't need to read input or print anything. Your task is to complete the function canTrade() which take four arguments. An array  **beautifulness** , its length  **n** , an integer **q** and an array  **queries** . You need to return the array of size q containing 0 and/or 1.

**Constraints:**
 - 1 <= n <= 10^5
 - 1 <= beautifulness[i] <= 10^9
 - 1 <= q <= 10^5
 - 1 <= queries[i][0] <= queries[i][1] <= N


## Solution:

## Method 1:

```java
import java.io.*;
import java.util.*;

public class Main {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int t = Integer.parseInt(br.readLine());

        while (t-- > 0) {
            int n = Integer.parseInt(br.readLine());
            int[] beautifulness = new int[n];
            StringTokenizer st = new StringTokenizer(br.readLine());

            for (int i = 0; i < n; i++) {
                beautifulness[i] = Integer.parseInt(st.nextToken());
            }

            int q = Integer.parseInt(br.readLine());
            int[][] queries = new int[q][2];

            for (int i = 0; i < q; i++) {
                st = new StringTokenizer(br.readLine());
                queries[i][0] = Integer.parseInt(st.nextToken());
                queries[i][1] = Integer.parseInt(st.nextToken());
            }

            int[] ans = Solution.canTrade(n, beautifulness, q, queries);

            for (int num : ans) {
                System.out.print(num + " ");
            }
            System.out.println();
        }
    }
}

class Solution {
    public static int[] canTrade(int n, int[] beautifulness, int q, int[][] queries) {
        int[] result = new int[q];
        int previous = beautifulness[0];
        beautifulness[0] = 0;
  
        for (int i = 1; i < n; i++) {
            int current = beautifulness[i];
            if (beautifulness[i] == previous) {
                beautifulness[i] = beautifulness[i-1];
            } else {
                beautifulness[i] = i;
            }
            previous = current;
        }
  
        for (int i = 0; i < q; i++) {
            int u = queries[i][0] - 1;
            int v = queries[i][1] - 1;
  
            result[i] = (beautifulness[v] <= u) ? 1 : 0;
        }
  
        return result;
    }
}

```
