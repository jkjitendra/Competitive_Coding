# Max Candies

## Problem Statement:

Candyman is a superhero who loves to see children happy and smiling. In order to achieve his dream, he decides to open a candy store, where he will have **N** candy containers. On each day, he decides to take a container and distrubute half the number of candies in that container. This goes on for M days.

Since seeing a child happy makes Candyman happy, he wants to maximize the total number of candies distributed to children.

Write a program to find the maximum number of candies that CandyMan can distribute.

**Input Format**

- The first line contains an integer **N**.
- Next, **N** lines contain **N** integers, where the **i`<sup>`th`</sup>`** value is the number of candies in the **i`<sup>`th`</sup>`** container.
- The last line of input contains an integer **M**, the number of days available to the CandyMan.

**Constraints**

- 1 <= N, M <= 10`<sup>`5`</sup>`
- 1 <= A[i] <= 10`<sup>`5`</sup>`

**Output Format**

- Print a single integer, the answer to the problem.

**Evaluation Parameters**

- Sample Input

```
4
6
2
3
5
6
```

- Sample Output

```
9
```

- Explanation
```
Day 1: Take 3 candies from container 1
Day 2: Take 2 candies from container 4
Day 3: Take 1 candy from container 1
Day 4: Take 1 candy from container 3
Day 5: Take 1 candy from container 4
Day 6: Take 1 candy from container 2
Total Candies = 9
```


## Solution:

#### Method 1:

```java
public class Result {
    public static long maxCandies(List<Integer> array, int m) {
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());
        maxHeap.addAll(array);

        for (int i = 0; i < m; i++) {
            int candies = maxHeap.poll();
            totalCandies += candies/2;
            maxHeap.add(candies - candies/2);
        }
        return totalCandies;
    }
}
```
