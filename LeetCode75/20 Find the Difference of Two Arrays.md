# Find the Difference of Two Arrays

## Problem Statement:

Given two **0-indexed** integer arrays `nums1` and `nums2`, return *a list* `answer` *of size* `2` *where:*

* `answer[0]` *is a list of all **distinct** integers in* `nums1` *which are **not** present in* `nums2`*.*
* `answer[1]` *is a list of all **distinct** integers in* `nums2` *which are **not** present in* `nums1`.

**Note** that the integers in the lists may be returned in **any** order.

**Example 1:**

<pre><strong>Input:</strong> nums1 = [1,2,3], nums2 = [2,4,6]
<strong>Output:</strong> [[1,3],[4,6]]
<strong>Explanation:
</strong>For nums1, nums1[1] = 2 is present at index 0 of nums2, whereas nums1[0] = 1 and nums1[2] = 3 are not present in nums2. Therefore, answer[0] = [1,3].
For nums2, nums2[0] = 2 is present at index 1 of nums1, whereas nums2[1] = 4 and nums2[2] = 6 are not present in nums2. Therefore, answer[1] = [4,6].</pre>

**Example 2:**

<pre><strong>Input:</strong> nums1 = [1,2,3,3], nums2 = [1,1,2,2]
<strong>Output:</strong> [[3],[]]
<strong>Explanation:
</strong>For nums1, nums1[2] and nums1[3] are not present in nums2. Since nums1[2] == nums1[3], their value is only included once and answer[0] = [3].
Every integer in nums2 is present in nums1. Therefore, answer[1] = [].
</pre>

**Constraints:**

* `1 <= nums1.length, nums2.length <= 1000`
* `-1000 <= nums1[i], nums2[i] <= 1000`

## Solution:

#### Method 1:

```java
class Solution {
    public List<List<Integer>> findDifference(int[] nums1, int[] nums2) {
        boolean[] nums1Array = new boolean[2001];
        boolean[] nums2Array = new boolean[2001];
        List<Integer> answer0 = new ArrayList<>();
        List<Integer> answer1 = new ArrayList<>();
        List<List<Integer>> answer = new ArrayList<>();
        for (int num : nums1) {
            nums1Array[num+1000] = true;
        }
        for (int num : nums2) {
            nums2Array[num+1000] = true;
        }
        for (int i = 0; i < 2001; i++) {
            if (nums1Array[i] && !nums2Array[i]) answer0.add(i-1000);
            if (nums2Array[i] && !nums1Array[i]) answer1.add(i-1000);
        }
        answer.add(answer0);
        answer.add(answer1);
        return answer;
}
```
