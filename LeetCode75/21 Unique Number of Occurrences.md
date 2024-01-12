# Unique Number of Occurrences

## Problem Statement:

Given an array of integers `arr`, return `true` *if the number of occurrences of each value in the array is **unique** or *`false` * otherwise* .

**Example 1:**

<pre><strong>Input:</strong> arr = [1,2,2,1,1,3]
<strong>Output:</strong> true
<strong>Explanation:</strong> The value 1 has 3 occurrences, 2 has 2 and 3 has 1. No two values have the same number of occurrences.</pre>

**Example 2:**

<pre><strong>Input:</strong> arr = [1,2]
<strong>Output:</strong> false
</pre>

**Example 3:**

<pre><strong>Input:</strong> arr = [-3,0,1,-3,1,1,1,-3,10,0]
<strong>Output:</strong> true
</pre>

**Constraints:**

* `1 <= arr.length <= 1000`
* `-1000 <= arr[i] <= 1000`


## Solution:

#### Method 1:

```java
  import java.util.Map.Entry;

  class Solution {
    public boolean uniqueOccurrences(int[] arr) {
      Map<Integer, Integer> occurrencesMap = new HashMap();
      boolean flag = true;
  
      for (int num: arr) {
        occurrencesMap.put(num, occurrencesMap.getOrDefault(num, 0) + 1);
      }

      ArrayList<Integer> listOfValues = new ArrayList<>();
      for (Map.Entry<Integer, Integer> entry : occurrencesMap.entrySet()) {
        listOfValues.add(entry.getValue());
      }

      Collections.sort(listOfValues);
      int n = listOfValues.size();
      for (int i = 0; i < n-1; i++) {
        if (listOfValues.get(i) == listOfValues.get(i+1)) {
          flag = false;
        }
      }
  
      return flag;
    }
  }
```


#### Method 2:

```java
  import java.util.Map.Entry;

  class Solution {
    public boolean uniqueOccurrences(int[] arr) {
      Map<Integer, Integer> occurrencesMap = new HashMap();
      HashSet<Integer> uniqueSetOfValues = new HashSet<>();
      for (int num: arr) {
        occurrencesMap.put(num, occurrencesMap.getOrDefault(num, 0) + 1);
      }
      for (Map.Entry<Integer, Integer> entry: occurrencesMap.entrySet()) {
        if(!uniqueSetOfValues.add(entry.getValue())) return false;
      }
      return true;
    }
  }
```
