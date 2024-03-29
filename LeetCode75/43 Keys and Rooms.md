# Keys and Rooms

## Problem Statement:

There are `n` rooms labeled from `0` to `n - 1` and all the rooms are locked except for room `0`. Your goal is to visit all the rooms. However, you cannot enter a locked room without having its key.

When you visit a room, you may find a set of **distinct keys** in it. Each key has a number on it, denoting which room it unlocks, and you can take all of them with you to unlock the other rooms.

Given an array `rooms` where `rooms[i]` is the set of keys that you can obtain if you visited room `i`, return `true` *if you can visit **all** the rooms, or* `false`  *otherwise* .

**Example 1:**

<pre><strong>Input:</strong> rooms = [[1],[2],[3],[]]
<strong>Output:</strong> true
<strong>Explanation:</strong> 
We visit room 0 and pick up key 1.
We then visit room 1 and pick up key 2.
We then visit room 2 and pick up key 3.
We then visit room 3.
Since we were able to visit every room, we return true.
</pre>

**Example 2:**

<pre><strong>Input:</strong> rooms = [[1,3],[3,0,1],[2],[0]]
<strong>Output:</strong> false
<strong>Explanation:</strong> We can not enter room number 2 since the only key that unlocks it is in that room.
</pre>

**Constraints:**

* `n == rooms.length`
* `2 <= n <= 1000`
* `0 <= rooms[i].length <= 1000`
* `1 <= sum(rooms[i].length) <= 3000`
* `0 <= rooms[i][j] < n`
* All the values of `rooms[i]` are  **unique** .


## Solution:

#### Method 1:

```java
class Solution {
  public boolean canVisitAllRooms(List<List<Integer>> rooms) {
    Set<Integer> visited = new HashSet<>();
    Stack<Integer> stack = new Stack<>();
    stack.push(0);
    visited.add(0);
    while (!stack.isEmpty()) {
      int currentRoom = stack.pop();
      for (int key : rooms.get(currentRoom)) {
        if (!visited.contains(key)) {
          visited.add(key);
          stack.push(key);
        }
      }
    }
    return visited.size() == rooms.size();
  }
}
```

#### Method 2:

```java
class Solution {
  public boolean canVisitAllRooms(List<List<Integer>> rooms) {
    boolean[] visited = new boolean[rooms.size()];
    int totalVisitedRooms = calculateTotalVisitedRooms(0, rooms,visited, 0);
    return totalVisitedRooms == rooms.size();
  }

  public int calculateTotalVisitedRooms(int key, List<List<Integer>> rooms, boolean[]visited, int count) {
    visited[key] = true;
    count++;
    for (int room : rooms.get(key)) {
      if (!visited[room]) {
        count = calculateTotalVisitedRooms(room, rooms, visited, count);
      }
    }
    return count;
  }
}

```
