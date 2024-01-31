# Total Cost to Hire K Workers

## Problem Statement:

You are given a **0-indexed** integer array `costs` where `costs[i]` is the cost of hiring the `i<sup>th</sup>` worker.

You are also given two integers `k` and `candidates`. We want to hire exactly `k` workers according to the following rules:

* You will run `k` sessions and hire exactly one worker in each session.
* In each hiring session, choose the worker with the lowest cost from either the first `candidates` workers or the last `candidates` workers. Break the tie by the smallest index.
  * For example, if `costs = [3,2,7,7,1,2]` and `candidates = 2`, then in the first hiring session, we will choose the `4<sup>th</sup>` worker because they have the lowest cost `[<u>3,2</u>,7,7,<u><strong>1</strong>,2</u>]`.
  * In the second hiring session, we will choose `1<sup>st</sup>` worker because they have the same lowest cost as `4<sup>th</sup>` worker but they have the smallest index `[<u>3,<strong>2</strong></u>,7,<u>7,2</u>]`. Please note that the indexing may be changed in the process.
* If there are fewer than candidates workers remaining, choose the worker with the lowest cost among them. Break the tie by the smallest index.
* A worker can only be chosen once.

Return *the total cost to hire exactly *`k`* workers.*

**Example 1:**

<pre><strong>Input:</strong> costs = [17,12,10,2,7,2,11,20,8], k = 3, candidates = 4
<strong>Output:</strong> 11
<strong>Explanation:</strong> We hire 3 workers in total. The total cost is initially 0.
- In the first hiring round we choose the worker from [<u>17,12,10,2</u>,7,<u>2,11,20,8</u>]. The lowest cost is 2, and we break the tie by the smallest index, which is 3. The total cost = 0 + 2 = 2.
- In the second hiring round we choose the worker from [<u>17,12,10,7</u>,<u>2,11,20,8</u>]. The lowest cost is 2 (index 4). The total cost = 2 + 2 = 4.
- In the third hiring round we choose the worker from [<u>17,12,10,7,11,20,8</u>]. The lowest cost is 7 (index 3). The total cost = 4 + 7 = 11. Notice that the worker with index 3 was common in the first and last four workers.
The total hiring cost is 11.
</pre>

**Example 2:**

<pre><strong>Input:</strong> costs = [1,2,4,1], k = 3, candidates = 3
<strong>Output:</strong> 4
<strong>Explanation:</strong> We hire 3 workers in total. The total cost is initially 0.
- In the first hiring round we choose the worker from [<u>1,2,4,1</u>]. The lowest cost is 1, and we break the tie by the smallest index, which is 0. The total cost = 0 + 1 = 1. Notice that workers with index 1 and 2 are common in the first and last 3 workers.
- In the second hiring round we choose the worker from [<u>2,4,1</u>]. The lowest cost is 1 (index 2). The total cost = 1 + 1 = 2.
- In the third hiring round there are less than three candidates. We choose the worker from the remaining workers [<u>2,4</u>]. The lowest cost is 2 (index 0). The total cost = 2 + 2 = 4.
The total hiring cost is 4.
</pre>

**Constraints:**

* `1 <= costs.length <= 10<sup>5 </sup>`
* `1 <= costs[i] <= 10<sup>5</sup>`
* `1 <= k, candidates <= costs.length`

## Solution:

#### Method 1:

```java
class Solution {
  public long totalCost(int[] costs, int k, int candidates) {
    long totalCostToHire = 0;
    int costLength = costs.length;  
    Queue<Integer> leftPriorityQueue = new PriorityQueue<>();
    Queue<Integer> rightPriorityQueue = new PriorityQueue<>();

    int startingIndex = candidates;
    for (int i = 0; i < candidates; i++) {
      leftPriorityQueue.add(costs[i]);
    }

    int endingIndex = Math.max(costLength - candidates, candidates) - 1;
    for (int i = costLength-1; i >= endingIndex+1; i--) {
      rightPriorityQueue.add(costs[i]);
    }

    while (k-- > 0){
      int leftCost = leftPriorityQueue.isEmpty() ? Integer.MAX_VALUE : leftPriorityQueue.peek();
      int rightCost = rightPriorityQueue.isEmpty() ? Integer.MAX_VALUE : rightPriorityQueue.peek();

      if (leftCost <= rightCost) {
        totalCostToHire += leftPriorityQueue.poll();
        if (startingIndex <= endingIndex) {
          leftPriorityQueue.add(costs[startingIndex]);
        }
      } else {
        totalCostToHire += rightPriorityQueue.poll();
        if (startingIndex <= endingIndex) {
          rightPriorityQueue.add(costs[endingIndex]);
        }
      }
    }
    return totalCostToHire;
  }
}

```

#### Method 2:

```java
class Solution {
  public long totalCost(int[] costs, int k, int candidates) {
    long totalCostToHire = 0;

    int startIndex = candidates - 1;
    int endIndex = costs.length - candidates;

    if (startIndex >= endIndex) {
      endIndex = startIndex + 1;
    }

    int[] startCandidates = Arrays.copyOfRange(costs, 0, startIndex + 1);
    int[] endCandidates = Arrays.copyOfRange(costs, endIndex, costs.length);

    int startHeapSize = startCandidates.length;
    int endHeapSize = endCandidates.length;

    buildMinHeap(startCandidates);
    buildMinHeap(endCandidates);

    while (k > 0) {
      int minStartCost = startCandidates[0];
      int minEndCost = endCandidates.length > 0 ? endCandidates[0] : Integer.MAX_VALUE;

      if (startHeapSize == 0) minStartCost = Integer.MAX_VALUE;
      if (endHeapSize == 0) minEndCost = Integer.MAX_VALUE;

      if (minStartCost <= minEndCost) {
        totalCostToHire += minStartCost;
        if (startIndex < endIndex - 1) {
          startCandidates[0] = costs[++startIndex];
          minHeapify(0, startCandidates, candidates);
        } else {
          swap(startCandidates, 0, startHeapSize - 1);
          minHeapify(0, startCandidates, --startHeapSize);
        }
      } else {
        totalCostToHire += minEndCost;
        if (endIndex > startIndex + 1) {
          endCandidates[0] = costs[--endIndex];
          minHeapify(0, endCandidates, candidates);
        } else {
          swap(endCandidates, 0, endHeapSize - 1);
          minHeapify(0, endCandidates, --endHeapSize);
        }
      }
      k--;
    }
    return totalCostToHire;
  }

  void buildMinHeap(int[] array) {
    for (int i = (array.length - 1) / 2; i >= 0; i--) {
      minHeapify(i, array, array.length);
    }
  }

  void minHeapify(int index, int[] array, int heapSize) {
    int leftChildIndex = 2 * index + 1;
    int rightChildIndex = 2 * index + 2;
    int smallestIndex = index;

    if (leftChildIndex < heapSize && array[leftChildIndex] < array[smallestIndex]) {
      smallestIndex = leftChildIndex;
    }
    if (rightChildIndex < heapSize && array[rightChildIndex] < array[smallestIndex]) {
      smallestIndex = rightChildIndex;
    }

    if (smallestIndex == index) return;
    swap(array, index, smallestIndex);
    minHeapify(smallestIndex, array, heapSize);
  }

  void swap(int[] array, int firstIndex, int secondIndex) {
    int temp = array[firstIndex];
    array[firstIndex] = array[secondIndex];
    array[secondIndex] = temp;
  }
}

```
