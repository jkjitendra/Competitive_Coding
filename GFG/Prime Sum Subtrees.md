## Prime Sum Subtrees

## Problem Statement:

Given a tree consisting of **n** nodes and **n-1** edges, where the nodes are labelled from **1 to n** and the root node is labelled **1**, the objective is to determine the count of **good subtrees** in the tree.

A subtree is called good if summation of all node values in that subtree, modulo **10<sup>5</sup>+3**, becomes a **prime number.**

**Example 1:**

```
Input:
N = 3
k = 1
edges=[[1,3],[1,2]]
Output:
2
Explanation:
The tree formed using the given edges is as shown below:
    1
   / \
  3   2
The subtree having the root node as 2, has sum 2.
The subtree having the root node as 3, has sum 3.
As 2 and 3 are prime numbers, so there are 2 subtrees in this tree which sum to a prime number.
```

**Example 2:**

```
Input:
N = 5
k = 4
edges=[[1,2],[1,3],[2,4],[2,5]]
Output:
3
Explanation:
The tree formed using the given edges is as shown below:
        1
       / \
      2   3
     / \
    4   5
The subtree having the root node as 5, has sum 5.
The subtree having the root node as 3, has sum 3.
The subtree having the root node as 2, has sum 11.
As 3,5 and 11 are prime numbers, so there are 3 subtrees in this tree which sum to a prime number.
```

**Your Task:**

You don't have to take input or print anything. Complete the function **primeSumSubtrees()** which takes the input parameters, an integer **n** and the **edges of the tree** as a 2-D integer array, representing the number of nodes, and returns an integer denoting the answer to the question.

**Constraints:**

1<=n<=10<sup>5</sup>

## Solution:

#### Method 1:

```java
import java.io.*;
import java.util.*;
import java.math.BigInteger;

public class GFG {
    public static void main(String[] args) throws IOException {
        Scanner sc=new Scanner(System.in);
        int t=sc.nextInt();
        while(t-- > 0){
            
            int n=sc.nextInt();
            int [][]edges=new int[n-1][2];
            for(int i=0;i<n-1;i++)
            {
                int a=sc.nextInt();
                int b=sc.nextInt();
                edges[i][0]=a;
                edges[i][1]=b;
            }
            Solution s=new Solution();
            int res = s.primeSumSubtrees(n,edges);
            System.out.println(res);
        }
    }
}

class Solution {
    private boolean[] prime = new boolean[100004];
    
    private void calculatePrimes() {
        Arrays.fill(prime, true);
        prime[0] = prime[1] = false;
        for (int p = 2; p * p < prime.length; p++) {
            if (prime[p]) {
                for (int i = p * p; i < prime.length; i += p) {
                    prime[i] = false;
                }
            }
        }
    }

    private int fun(int node, ArrayList<ArrayList<Integer>> adj, boolean[] visited, int[] ans) {
        visited[node] = true;
        int subtreeSum = node;
        for (int child : adj.get(node)) {
            if (!visited[child]) {
                subtreeSum = (subtreeSum + fun(child, adj, visited, ans)) % 100003;
            }
        }
        if (prime[subtreeSum]) {
            ans[0]++;
        }
        return subtreeSum;
    }
    
    public int primeSumSubtrees(int n, int[][] edges) {
        // code here
        calculatePrimes();
        ArrayList<ArrayList<Integer>> adj = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            adj.add(new ArrayList<>());
        }
        for (int[] edge : edges) {
            int u = edge[0];
            int v = edge[1];
            adj.get(u).add(v);
            adj.get(v).add(u);
        }
        boolean[] visited = new boolean[n + 1];
        int[] ans = new int[1]; // Use an array to hold the count
        fun(1, adj, visited, ans);
        return ans[0];
    }
}
```