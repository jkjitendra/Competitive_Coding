# Tasty Dishes

## Problem Statement

There are N dishes in a line. You are given two arrays size and taste. For all i(1<= i <= N), size[i] denotes the size of the ith dish and taste[i] denotes the taste of the ith dish. You are allowed to eat at most M dishes. The satisfaction of eating some dishes is given as follows:

 - Say if you eat `k` different dishes, then the value of satisfaction will be equal to the sum of the sizes of all `k` dishes multiplied by the minimuim taste among all the k dishes.

 Calculate the maximum satisfaction you can get after eating at most M different dishes.

 **Function description**

 Complete the function `solve`. This function takes the following 4 parameters and returns the required answer:

 - N: Represents the total number of dishes
 - M: Represents the maximum number of dishes you can eat
 - size: Represents an array of sizes N denoting the sizes of the dishes
 - taste: Represents an array of sizes N denoting the tastes of the dishes

 **Input format for custom testing**<br>
 **Note**: Use this input format if you are testing against custom input or writing code in a language where we don't provide boilerplate code.

 - The first line contains T, which represents the number of test cases.
 - For each test case:
   - The first line contains an integer N denoting the total number of dishes.
   - The second line contains an integer M, denoting the maximum number of dishes that can be eaten.
   - The third line contains N space-separated integers denoting the elements of size.
   - The fourth line contains N space-separated integers denoting the elements of taste.

**Output Format**<br>
For each test case in a new line, print an integer representing the maximum satisfaction as the answer.

**Constraints:**

1 <= T <= 10<br/>
1 <= N <= 10^5<br/>
1 <= M <= N<br/>
1 <= size[i] <= 10^6<br/>
1 <= taste[i] <= 10^6<br/>

**Sample Input**<br/>
1<br/>
5<br/>
2<br/>
10 7 8 11 1<br/>
3 5 1 6 9<br/>

**Sample Output**<br/>
90

**Explanation**

The first line contains the number of test cases, T = 1.

**The first test case**

Given<br/>
 - N = 5
 - M = 2
 - size = [10, 7, 8, 11, 1]
 - taste = [3, 5, 1, 6, 9]

 Approach
 - Among all the pairs if you eat, 2<sup>nd</sup> and the 4<sup>th</sup> dish, the satisfaction will be = (7 + 11) * 5 = 90, which is the maximum.
 - So, the answer will be 90.

**Note**:

Your code must be able to print the sample output from the provided sample input. However, your code is run against multiple hidden test cases. Therefore, your code must pass these hidden test cases to solve the problem statement.

## Solution

#### Method 1:

```java
import java.io.*;
import java.util.*;

public class TestClass {
    public static void main(String[] args) throws IOException {
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        PrintWriter wr = new PrintWriter(System.out);
        int T = Integer.parseInt(br.readLine().trim());
        for (int t_i = 0; t_i < T; t_i++) {
            int N = Integer.parseInt(br.readLine().trim());
            int M = Integer.parseInt(br.readLine().trim());
            String[] arr_size = br.readLine().split(" ");
            int[] size = new int[N];
            for (int i_size = 0; i_size < arr_size.length; i_size++) {
                size[i_size] = Integer.parseInt(arr_size[i_size]);
            }
            String[] arr_taste = br.readLine().split(" ");
            int[] taste = new int[N];
            for (int i_taste = 0; i_taste < arr_taste.length; i_taste++) {
                taste[i_taste] = Integer.parseInt(arr_taste[i_taste]);
            }

            long out_ = solve(N, M, size, taste);
            System.out.println(out_);
        }

        wr.close();
        br.close();
    }

    static long solve(int N, int M, int[] size, int[] taste) {
        long result = 0;

        // Create a list of dishes with both size and taste as pairs
        int[][] dishes = new int[N][2];
        for (int i = 0; i < N; i++) {
            dishes[i][0] = size[i];
            dishes[i][1] = taste[i];
        }

        // Sort dishes by taste in descending order
        Arrays.sort(dishes, (d1, d2) -> d2[1] - d1[1]);

        // Priority queue to keep track of the largest sizes
        PriorityQueue<Integer> pq = new PriorityQueue<>();
        long sumOfSizes = 0;

        for (int i = 0; i < N; i++) {
            int currentSize = dishes[i][0];
            int currentTaste = dishes[i][1];

            if (pq.size() < M) {
                pq.add(currentSize);
                sumOfSizes += currentSize;
            } else if (!pq.isEmpty() && currentSize > pq.peek()) {
                sumOfSizes -= pq.poll();
                pq.add(currentSize);
                sumOfSizes += currentSize;
            }
            if (pq.size() == M) {
                result = Math.max(result, sumOfSizes * currentTaste);
            }
        }

        return result;
    }
}
```