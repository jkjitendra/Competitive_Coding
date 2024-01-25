# Evaluate Division

## Problem Statement:

You are given an array of variable pairs `equations` and an array of real numbers `values`, where `equations[i] = [A<sub>i</sub>, B<sub>i</sub>]` and `values[i]` represent the equation `A<sub>i</sub> / B<sub>i</sub> = values[i]`. Each `A<sub>i</sub>` or `B<sub>i</sub>` is a string that represents a single variable.

You are also given some `queries`, where `queries[j] = [C<sub>j</sub>, D<sub>j</sub>]` represents the `j<sup>th</sup>` query where you must find the answer for `C<sub>j</sub> / D<sub>j</sub> = ?`.

Return  *the answers to all queries* . If a single answer cannot be determined, return `-1.0`.

**Note:** The input is always valid. You may assume that evaluating the queries will not result in division by zero and that there is no contradiction.

**Note: **The variables that do not occur in the list of equations are undefined, so the answer cannot be determined for them.

**Example 1:**

<pre><strong>Input:</strong> equations = [["a","b"],["b","c"]], values = [2.0,3.0], queries = [["a","c"],["b","a"],["a","e"],["a","a"],["x","x"]]
<strong>Output:</strong> [6.00000,0.50000,-1.00000,1.00000,-1.00000]
<strong>Explanation:</strong> 
Given: <em>a / b = 2.0</em>, <em>b / c = 3.0</em>
queries are: <em>a / c = ?</em>, <em>b / a = ?</em>, <em>a / e = ?</em>, <em>a / a = ?</em>, <em>x / x = ? </em>
return: [6.0, 0.5, -1.0, 1.0, -1.0 ]
note: x is undefined => -1.0</pre>

**Example 2:**

<pre><strong>Input:</strong> equations = [["a","b"],["b","c"],["bc","cd"]], values = [1.5,2.5,5.0], queries = [["a","c"],["c","b"],["bc","cd"],["cd","bc"]]
<strong>Output:</strong> [3.75000,0.40000,5.00000,0.20000]
</pre>

**Example 3:**

<pre><strong>Input:</strong> equations = [["a","b"]], values = [0.5], queries = [["a","b"],["b","a"],["a","c"],["x","y"]]
<strong>Output:</strong> [0.50000,2.00000,-1.00000,-1.00000]
</pre>

**Constraints:**

* `1 <= equations.length <= 20`
* `equations[i].length == 2`
* `1 <= A<sub>i</sub>.length, B<sub>i</sub>.length <= 5`
* `values.length == equations.length`
* `0.0 < values[i] <= 20.0`
* `1 <= queries.length <= 20`
* `queries[i].length == 2`
* `1 <= C<sub>j</sub>.length, D<sub>j</sub>.length <= 5`
* `A<sub>i</sub>, B<sub>i</sub>, C<sub>j</sub>, D<sub>j</sub>` consist of lower case English letters and digits.


## Solution:

#### Method 1:

```java
class Solution {
  public double[] calcEquation(List<List<String>> equations, double[] values, List<List<String>> queries) {
    Map<String, Map<String, Double>> divisionGraph = buildDivisionGraph(equations, values);
    double[] queryResults = new double[queries.size()];

    for (int i = 0; i < queries.size(); i++) {
      List<String> query = queries.get(i);
      queryResults[i] = calculateDivisionResult(query.get(0), query.get(1), divisionGraph, new HashSet<>());
    }
    return queryResults;
  }

  private Map<String, Map<String, Double>> buildDivisionGraph(List<List<String>> equations, double[] values) {
    Map<String, Map<String, Double>> divisionGraph = new HashMap<>();
    for (int i = 0; i < equations.size(); i++) {
      String numerator = equations.get(i).get(0);
      String denominator = equations.get(i).get(1);
      divisionGraph.computeIfAbsent(numerator, k -> new HashMap<>()).put(denominator, values[i]);
      divisionGraph.computeIfAbsent(denominator, k -> new HashMap<>()).put(numerator, 1.0 / values[i]);
    }
    return divisionGraph;
  }

  private double calculateDivisionResult(String numerator, String denominator, Map<String, Map<String, Double>> divisionGraph, Set<String> visited) {
    if (!divisionGraph.containsKey(numerator) || !divisionGraph.containsKey(denominator)) {
      return -1.0;
    }
    if (numerator.equals(denominator)) {
      return 1.0;
    }

    visited.add(numerator);
    Map<String, Double> adjacentVertices = divisionGraph.get(numerator);
    for (String adjacentVertex : adjacentVertices.keySet()) {
      if (!visited.contains(adjacentVertex)) {
        double adjacentValue = calculateDivisionResult(adjacentVertex, denominator, divisionGraph, visited);
        if (adjacentValue != -1.0) {
          return adjacentVertices.get(adjacentVertex) * adjacentValue;
        }
      }
    }
    return -1.0;
  }
}

```




#### Method 2:

```java

```
