# Daily Temperatures

## Problem Statement:

Given an array of integers `temperatures` represents the daily temperatures, return *an array* `answer` *such that* `answer[i]` *is the number of days you have to wait after the* `i<sup>th</sup>`  *day to get a warmer temperature* . If there is no future day for which this is possible, keep `answer[i] == 0` instead.

**Example 1:**

<pre><strong>Input:</strong> temperatures = [73,74,75,71,69,72,76,73]
<strong>Output:</strong> [1,1,4,2,1,1,0,0]
</pre>

**Example 2:**

<pre><strong>Input:</strong> temperatures = [30,40,50,60]
<strong>Output:</strong> [1,1,1,0]
</pre>

**Example 3:**

<pre><strong>Input:</strong> temperatures = [30,60,90]
<strong>Output:</strong> [1,1,0]
</pre>

**Constraints:**

* `1 <= temperatures.length <= 10<sup>5</sup>`
* `30 <= temperatures[i] <= 100`

## Solution:

#### Method 1:

```java
class Solution {
  public int[] dailyTemperatures(int[] temperatures) {
    int n = temperatures.length;
    int[] warmerTemperatures = new int[n];
    for (int i = 0; i < n; i++) {
      int count = 0;
      for (int j = i+1; j< n; j++) {
        count++;
        if (temperatures[i] < temperatures[j]) {
          warmerTemperatures[i] = count;
          break;
        }
      }
    }
    return warmerTemperatures;
  }
}
```

#### Method 2:

```java
class Solution {
  public int[] dailyTemperatures(int[] temperatures) {
    int n = temperatures.length;
    int[] warmerTemperatures = new int[n];
    Stack<Integer> stack = new Stack<>();

    for (int i = 0; i < n; i++) {
      while (!stack.isEmpty() && temperatures[stack.peek()] < temperatures[i]) {
        warmerTemperatures[stack.peek()] = i - stack.pop();
      }
      stack.push(i);
    }
    return warmerTemperatures;
  }
}
```

#### Method 3:

```java
class Solution {
  public int[] dailyTemperatures(int[] temperatures) {
    int n = temperatures.length;
    int[] warmerTemperatures = new int[n];
    Stack<Integer> stack = new Stack<>();

    for (int i = n - 2; i >= 0; i--) {
      int j = i + 1;
      while (j < n && temperatures[i] >= temperatures[j]) {
        if (warmerTemperatures[j] > 0) {
          // Jump ahead by the number of days stored in answer[j]
          j += warmerTemperatures[j];
        } else {
          // If answer[j] is 0, there are no warmer days ahead of j
          break;
        }
      }
      // If we found a warmer day, update answer[i] with the distance to that day
      if (j < n && temperatures[i] < temperatures[j]) {
        warmerTemperatures[i] = j - i;
      }
    }
    return warmerTemperatures;
  }
}
```

#### Method 4:

```java
import java.util.Arrays;

class Solution {
  public int[] dailyTemperatures(int[] temperatures) {
    int n = temperatures.length;
    int[] warmerTemperatures = new int[n];
    int nextWarmerDayTemperature = Integer.MIN_VALUE;

    for (int i = n - 1; i >= 0; i--) {
      if (temperatures[i] < nextWarmerDayTemperature) {
        // If current temperature is less than the next warmer day's temperature,
        // find how many days until the warmer temperature.
        int days = 1;
        while (temperatures[i] >= temperatures[i + days]) {
          // Use the answer array to skip days.
          days += warmerTemperatures[i + days];
        }
        warmerTemperatures[i] = days;
      }
      // Update the nextWarmerDayTemperature if current temperature is higher
      if (temperatures[i] > nextWarmerDayTemperature) {
        nextWarmerDayTemperature = temperatures[i];
      }
    }
    return warmerTemperatures;
  }
}
```
