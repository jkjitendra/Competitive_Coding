# N-th Tribonacci Number

## Problem Statement:

The Tribonacci sequence T~n~ is defined as follows:

T~0~ = 0, T~1~ = 1, T~2~ = 1, and T~n+3~ = T~n~ + T~n+1~ + T~n+2~ for n >= 0.

Given `n`, return the value of T ~n~ .

**Example 1:**

<pre><strong>Input:</strong> n = 4
<strong>Output:</strong> 4
<strong>Explanation:</strong>
T_3 = 0 + 1 + 1 = 2
T_4 = 1 + 1 + 2 = 4
</pre>

**Example 2:**

<pre><strong>Input:</strong> n = 25
<strong>Output:</strong> 1389537
</pre>

**Constraints:**

* `0 <= n <= 37`
* The answer is guaranteed to fit within a 32-bit integer, ie. `answer <= 2^31 - 1`.


## Solution:

#### Method 1:

```java
class Solution {
  public int tribonacci(int n) {
    int result = sequenceRecursive(n);
    return result;
  }

  private int sequenceRecursive(int n) {
    if (n <= 0) return 0;
    if (n == 1) return 1;
    if (n == 2) return 1;
    int res = 0;
    res += sequenceRecursive(n-1) + sequenceRecursive(n-2) + sequenceRecursive(n-3);
    return res;
  }
}
```


#### Method 2:
