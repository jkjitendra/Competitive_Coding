# Compute Bit Distance

## Problem Statement:

The bit distance, d, of an integer, x, is defined as the maximum distance between any two consecutive set bits. For example, let x = 1036, which, represented in binary, is 10000000100. The distances between consecutive set bits are 0 (6), respectively. Hence, the bit distance d is equal to 6. If there is only one set bit, the bit distance is considered to be -1. Given an integer array, the goal is to find the top k integers with maximum bit distances.

For the given array of integers, sort the integers in decreasing order of their bit distances. If there are multiple integers with the same bit distances, sort them in decreasing order by their value. Report the first k integers of the array thus obtained.

Example:
For example, let n = 5, numbers = [12, 4, 5, 10, 8], and k = 3.

The binary representation of array numbers is [1100, 100, 101, 1010, 1000]. The corresponding bit distances d are [0, -1, 1, 1, -1].

5 and 10 are the integers with the highest d value of 1, but since the value of 10 is greater than 5, 10 would be reported first. 5 is reported second.

The second-largest d value is for 12, with a bit distance of 0. Since there are no other integers with a d value of 0, 12 is reported third.

Hence, the final pick would be the integers [10, 5, 12].

**Function Description**
Complete the function getTopKBitDistances in the editor below.

getTopKBitDistances has the following parameters:

	•	INTEGER_ARRAY numbers: an array of positive integers
	•	INTEGER k: an integer denoting the number of integers you need to select

Returns:

	•	res: an array of k integers denoting the set of topmost k integers in decreasing order of their bit distances.

**Constraints:**

	•	1 <= n <= 10^5
	•	1 <= numbers[i] <= 10^8
	•	1 <= k <= n

**Input Format for Custom Testing:**
The first line contains an integer, n, denoting the number of elements in numbers.
Each line i of the n subsequent lines (where 0 <= i < n) contains a positive integer describing numbers[i].
The next line contains an integer, k, denoting the number of integers you need to select.

**Sample Case 0:**
Sample Input 0
```
numbers size is 3
numbers = [3, 5, 8]
k = 1
```

Sample Output 0
```
5
```

Explanation
The integers in binary form are [11, 101, 1000]. The corresponding d values are [0, 1, -1]. The bit distance of 3 is 0, the bit distance of 5 is 1, and the bit distance of 8 is 0. The maximum bit distance is 1, and the only integer with this bit distance is 5.
Since k = 1, only the integer with the highest bit distance is reported, which is 5. Hence, the final pick would be the integer [5].

**Sample Case 1:**
Sample Input 1
```
numbers size is 4
numbers = [10, 13, 5, 18]
k = 3
```

Sample Output 1
```
18, 13, 10
```

Explanation:
The integers in binary form are [1010, 1101, 101, 10010]. The corresponding d values are [1, 1, 1, 2]. 18 is reported first because it has the highest d value. 10, 13, and 5 all have the same bit distance, and since only 2 more integers need to be reported, 13 and 10 are reported in that order because those are the two largest integers in decreasing order. Hence, the answer is [18, 13, 10].

## Solution:

#### Method 1:
```java

public class Result {

    private static int computeBitDistance(int num) {
        String binary = Integer.toBinaryString(num);
        int maxDistance = -1;
        int lastSetBit = -1;

        for (int i = 0; i < binary.length(); i++) {
            if (binary.charAt(i) == '1') {
                if (lastSetBit != -1) {
                    maxDistance = Math.max(maxDistance, i - lastSetBit);
                }
                lastSetBit = i;
            }
        }

        return maxDistance;
    }

    public static List<Integer> getTopKBitDistances(List<Integer> numbers, int k) {
        List<int[]> numberBitDistancePairs = new ArrayList<>();

        for (int num : numbers) {
            int bitDistance = computeBitDistance(num);
            numberBitDistancePairs.add(new int[] {num, bitDistance});
        }

        numberBitDistancePairs.sort((a, b) -> {
            if (b[1] != a[1]) {
                return Integer.compare(b[1], a[1]); // Sort by bit distance
            } else {
                return Integer.compare(b[0], a[0]); // Sort by value
            }
        });

        // Extract the top K numbers
        List<Integer> result = new ArrayList<>();
        for (int i = 0; i < k; i++) {
            result.add(numberBitDistancePairs.get(i)[0]);
        }

        return result;
    }

    public static void main(String[] args) {
        List<Integer> numbers = Arrays.asList(10, 13, 5, 18);
        int k = 3;
        List<Integer> topK = getTopKBitDistances(numbers, k);
        System.out.println(topK);
    }
}
```