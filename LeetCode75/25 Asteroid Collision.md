# Asteroid Collision

## Problem Statement:

We are given an array `asteroids` of integers representing asteroids in a row.

For each asteroid, the absolute value represents its size, and the sign represents its direction (positive meaning right, negative meaning left). Each asteroid moves at the same speed.

Find out the state of the asteroids after all collisions. If two asteroids meet, the smaller one will explode. If both are the same size, both will explode. Two asteroids moving in the same direction will never meet.

**Example 1:**

<pre><strong>Input:</strong> asteroids = [5,10,-5]
<strong>Output:</strong> [5,10]
<strong>Explanation:</strong> The 10 and -5 collide resulting in 10. The 5 and 10 never collide.
</pre>

**Example 2:**

<pre><strong>Input:</strong> asteroids = [8,-8]
<strong>Output:</strong> []
<strong>Explanation:</strong> The 8 and -8 collide exploding each other.
</pre>

**Example 3:**

<pre><strong>Input:</strong> asteroids = [10,2,-5]
<strong>Output:</strong> [10]
<strong>Explanation:</strong> The 2 and -5 collide resulting in -5. The 10 and -5 collide resulting in 10.
</pre>

**Constraints:**

* `2 <= asteroids.length <= 10<sup>4</sup>`
* `-1000 <= asteroids[i] <= 1000`
* `asteroids[i] != 0`

## Solution:

#### Method 1:

```java
  class Solution {
    public int[] asteroidCollision(int[] asteroids) {
      int n = asteroids.length;
      Stack<Integer> stack = new Stack<>();

      for (int i = 0; i < n; i++) {
        int currentAsteroid = asteroids[i];
        if (currentAsteroid > 0) {
          stack.push(currentAsteroid);
        } else {
          while (!stack.isEmpty() && stack.peek() > 0 && stack.peek() + currentAsteroid < 0) {
            stack.pop();
          }
          if (stack.isEmpty() || stack.peek() < 0) {
            stack.push(currentAsteroid);
          } else if (stack.peek() + currentAsteroid == 0) {
            stack.pop();
          }
        }
      }
      int stackSize = stack.size();
      int[] stateOfAsteroid = new int[stackSize];
      for (int i = stackSize - 1; i >= 0; i--) {
        stateOfAsteroid[i] = stack.pop();
      }
      return stateOfAsteroid;
    }
  }
```


#### Method 2:

```java
  class Solution {
    public int[] asteroidCollision(int[] asteroids) {
      int topIndex = -1;
      for(int currentAsteroid : asteroids) {
        boolean isAlive = true;
        while(isAlive && currentAsteroid < 0 && topIndex >= 0 && asteroids[topIndex] > 0 ) {
          isAlive = (currentAsteroid + asteroids[topIndex]) < 0 ? true : false;
          if(currentAsteroid + asteroids[topIndex] <= 0) {
              topIndex--; 
          }
        }
        if(isAlive) {
          asteroids[++topIndex] = currentAsteroid;
        }
      }
      return Arrays.copyOf(asteroids , topIndex + 1);
    }
  }
```
