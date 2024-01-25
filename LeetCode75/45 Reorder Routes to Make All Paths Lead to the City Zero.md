# Reorder Routes to Make All Paths Lead to the City Zero

## Problem Statement:

There are `n` cities numbered from `0` to `n - 1` and `n - 1` roads such that there is only one way to travel between two different cities (this network form a tree). Last year, The ministry of transport decided to orient the roads in one direction because they are too narrow.

Roads are represented by `connections` where `connections[i] = [a<sub>i</sub>, b<sub>i</sub>]` represents a road from city `a<sub>i</sub>` to city `b<sub>i</sub>`.

This year, there will be a big event in the capital (city `0`), and many people want to travel to this city.

Your task consists of reorienting some roads such that each city can visit the city `0`. Return the **minimum** number of edges changed.

It's **guaranteed** that each city can reach city `0` after reorder.

**Example 1:**

![](https://assets.leetcode.com/uploads/2020/05/13/sample_1_1819.png)

<pre><strong>Input:</strong> n = 6, connections = [[0,1],[1,3],[2,3],[4,0],[4,5]]
<strong>Output:</strong> 3
<strong>Explanation: </strong>Change the direction of edges show in red such that each node can reach the node 0 (capital).
</pre>

**Example 2:**

![](https://assets.leetcode.com/uploads/2020/05/13/sample_2_1819.png)

<pre><strong>Input:</strong> n = 5, connections = [[1,0],[1,2],[3,2],[3,4]]
<strong>Output:</strong> 2
<strong>Explanation: </strong>Change the direction of edges show in red such that each node can reach the node 0 (capital).
</pre>

**Example 3:**

<pre><strong>Input:</strong> n = 3, connections = [[1,0],[2,0]]
<strong>Output:</strong> 0
</pre>

**Constraints:**

* `2 <= n <= 5 * 10<sup>4</sup>`
* `connections.length == n - 1`
* `connections[i].length == 2`
* `0 <= a<sub>i</sub>, b<sub>i</sub> <= n - 1`
* `a<sub>i</sub> != b<sub>i</sub>`

## Solution:

#### Method 1:

```java
class Solution {
  public int minReorder(int n, int[][] connections) {

    LinkedList<int[]>[] adjacencyList = new LinkedList[n];
    for(int i = 0; i != n; ++i) 
      adjacencyList[i] = new LinkedList<>();

    for(int[] connection: connections){
      int fromCity = connection[0];
      int toCity = connection[1];
      adjacencyList[fromCity].add(new int[]{toCity, 1});
      adjacencyList[toCity].add(new int[]{fromCity, 0});
    }  

    int[] visited = new int[n];
    int reorderRoadsCount = 0;
    LinkedList<Integer> queue = new LinkedList<>();
    queue.add(0);

    while(!queue.isEmpty()) { 
      int currentCity = queue.poll();
      if(visited[currentCity] == 1) continue;
      visited[currentCity] = 1;

      for(int[] road: adjacencyList[currentCity]) {
        if(visited[road[0]] == 0){
          queue.add(road[0]);
          if(road[1] == 1) ++reorderRoadsCount;
        }
      }
    }
    return reorderRoadsCount;
  }
}
```


#### Method 2:
