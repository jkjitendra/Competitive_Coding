# Number of Provinces

## Problem Statement:

There are `n` cities. Some of them are connected, while some are not. If city `a` is connected directly with city `b`, and city `b` is connected directly with city `c`, then city `a` is connected indirectly with city `c`.

A **province** is a group of directly or indirectly connected cities and no other cities outside of the group.

You are given an `n x n` matrix `isConnected` where `isConnected[i][j] = 1` if the `i<sup>th</sup>` city and the `j<sup>th</sup>` city are directly connected, and `isConnected[i][j] = 0` otherwise.

Return  *the total number of **provinces*** .

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/12/24/graph1.jpg)

<pre><strong>Input:</strong> isConnected = [[1,1,0],[1,1,0],[0,0,1]]
<strong>Output:</strong> 2
</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/12/24/graph2.jpg)

<pre><strong>Input:</strong> isConnected = [[1,0,0],[0,1,0],[0,0,1]]
<strong>Output:</strong> 3
</pre>

**Constraints:**

* `1 <= n <= 200`
* `n == isConnected.length`
* `n == isConnected[i].length`
* `isConnected[i][j]` is `1` or `0`.
* `isConnected[i][i] == 1`
* `isConnected[i][j] == isConnected[j][i]`

## Solution:

#### Method 1:

```java
class Solution {
  public int findCircleNum(int[][] isConnected) {
    int totalProvinces = 0;
    int n = isConnected.length;
    boolean visited[]=new boolean[n];
    int sourceCity = 0;
    while(sourceCity < n) {
      if(!visited[sourceCity]) {
        markCitiesVisitedInAProvince(sourceCity, isConnected, visited , n);
        totalProvinces++;
      }
      sourceCity++;
    }
    return totalProvinces;
  }

  public static void markCitiesVisitedInAProvince(int sourceCity, int[][] isConnected, boolean[] visited, int n) {
    visited[sourceCity]=true;
    int city = 0;
    while (city < n){
      if(!visited[city] && isConnected[sourceCity][city] == 1) {
        markCitiesVisitedInAProvince(city, isConnected, visited, n);
      }
      city++;
    }
  }
}

```

#### Method 2:

```java
class Solution {
  public int findCircleNum(int[][] isConnected) {
    int n = isConnected.length;
    boolean[] visited = new boolean[n];
    int totalProvinces = 0;
  
    for (int i = 0; i < n; i++) {
      if (!visited[i]) {
        totalProvinces++;
        Stack<Integer> stack = new Stack<>();
        stack.push(i);

        while (!stack.isEmpty()) {
          int node = stack.pop();
          visited[node] = true;
    
          for (int j = 0; j < n; j++) {
            if (isConnected[node][j] == 1 && !visited[j]) {
              stack.push(j);
            }
          }
        }
      }
    }
    return totalProvinces;
  }
}

```
