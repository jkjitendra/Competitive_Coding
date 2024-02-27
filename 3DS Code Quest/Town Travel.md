# Town Travel

## Problem Statement:

There are **n** towns numbered **1** to **n**, and **m** roads connecting them. Arrays **a** and **b** are given such that road **i** connects town **a[i]** and **b[i]**.

Your task is to return an array of size **m** whose **i`<sup>`th`</sup>`** element denotes the latest number of roads that would be used in travelling from town **1** to town **n** when the **i`<sup>`th`</sup>`** road cannot be used in the traversal. Return **-1** as the **i`<sup>`th`</sup>`** element if it is impossible to travel from town **1** to town **n** without using the **i`<sup>`th`</sup>`** road.

**Input Format**

- The first line contains the integer **n**, denoting the number of towns.
- The second line contains the integer **m**, denoting the number of roads.
- The next **m** lines contains the elements of the array **a**.
- The next line again contains the integer **m**, denoting the number of roads.
- The next **m** lines contain the elements of the array **b**.

**Constraints**

- 2 <= n <= 300
- 1 <= m <= n*(n-1)
- if (i != j) then (a[i], b[i]) != (a[j], b[j])
- a[i] != b[i]
- 1 <= a[i], b[i] <= n

**Output Format**

- Return an array as said in the problem statement.

**Evaluation Parameters**

- Sample Input

```
3
3
1
2
1
3
3
3
2
```

- Sample Output

```
2
1
1
```

- Explanation
```
Number of towns n = 3,
Number of roads m = 3,
array a: [1,2,1],
Number of roads m = 3,
array b: [3,3,2],

The graph is shown below:


            1
          /   \
         /     \
        3-------2
```

## Solution:

#### Method 1:

```java
class Result {

    // Method to remove the edge
    private static void removeEdge(List<List<Integer>> graph, int a, int b) {
        graph.get(a).remove((Integer) b);
        graph.get(b).remove((Integer) a);
    }

    // Method to add the edge
    private static void addEdge(List<List<Integer>> graph, int a, int b) {
        graph.get(a).add((Integer) b);
        graph.get(b).add((Integer) a);
    }

    // BFS method to find shortest path
    private static int bfs(List<List<Integer>> graph, int n, int source) {
        Queue<Integer> queue = new LinkedList<>();
        boolean[] visited = new boolean[n+1];
        int[] distance = new int[n+1];
        queue.offer(source);
        visited[source] = true;
        distance[source] = 0;

        while (!queue.isEmpty()) {
            int current = queue.poll();
            for (int neighbor : graph.get(current)) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    distance[neighbor] = distance[current] + 1;
                    queue.offer(neighbor);
                    if (neighbor == n) {
                        return distance[neighbor];
                    }
                }
            }
        }
        return -1; // No path found
    }

    // Main method to find shortest path with each road removed
    public static List<Integer> townTravel(int n, List<Integer> a, List<Integer> b) {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i <= n; i++) {
            graph.add(new ArrayList<>());
        }
        for (int i = 0; i < a.size(); i++) {
            graph.get(a.get(i)).add(b.get(i));
            graph.get(b.get(i)).add(a.get(i));
        }
        List<Integer> res = new ArrayList<>();

        for (int i = 0; i < a.size(); i++) {
            removeEdge(graph, a.get(i), b.get(i));

            int pathLength = bfs(graph, n, 1);

            res.add(pathLength);

            addEdge(graph, a.get(i), b.get(i));
        }
        return res;
    }

    // Example usage
    public static void main(String[] args) {
        List<Integer> a = Arrays.asList(1, 2, 1);
        List<Integer> b = Arrays.asList(3, 3, 2);
        List<Integer> result = townTravel(3, a, b);
        for (int num : result) {
            System.out.println(num);
        }
    }
}
```
