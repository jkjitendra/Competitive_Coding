# Optimizing Competition

## Problem Statement:

A thrilling boat competition is on the horizon, and N enthusiastic participants are eager to team up and participate. Each participant has a weight, represented by Wi. However, there is a catch - the competition only allows teams consisting of two participants. As an organizer, you want to ensure fairness by allowing only teams with the same total weight.

For instance, if there are K teams, each comprising participants (a1, b1), (a2, b2), ..., (ak, bk), where ai is the weight of the first participant in the i-th team, and bi is the weight of the second participant in the i-th team, a key condition needs to be satisfied: a1 + b1 = a2 + b2 = ... = ak + bk = s, where s is the common total weight of each team.

Your challenge is to find an optimal value for s such that the maximum possible number of teams can be formed. It is important to note that each participant can only be part of one team.

**Input Format**

The first line contains an integer N, the number of participants.

The second line contains N space-separated integers W1, W2, ..., WN, where wi represents the weight of the i-th participant.

**Output Format**
Print the maximum number of teams that can be formed with the optimal total weight s.

**Constraints**

- 1 ≤ N ≤ 50
- 1 ≤ Wi ≤ N

**Sample TestCase 1**

```
Input:
6
1 1 3 4 2 2

Output
2

Explanation

There are two possible cases:

Case 1: The value of s = 3
        Two teams can be formed (1, 2) and (1, 2).

Case 2: The value of s = 4
        Two teams can be formed (1, 3) and (2, 2).

In any case, the maximum number of valid teams formed are 2.
```

## Solution:

#### Method1:

```java
import java.io.*;
import java.util.*;

public class CandidateCode {
   public static void main(String args[] ) throws Exception {

      //Write code here
      Scanner sc = new Scanner(System.in);
      int N = sc.nextInt();
      
      int[] weights = new int[N];
      Map<Integer, Integer> weightFreq = new HashMap<>();
      
      for (int i = 0; i < N; i++) {
         weights[i] = sc.nextInt();
         weightFreq.put(weights[i], weightFreq.getOrDefault(weights[i], 0) + 1);
      }
      
      int maxTeams = 0;
      for (int s = 2; s <= 2 * N; s++) {
         int teamsForS = 0;
         for (int i = 1; i <= s / 2; i++) {
            if (i == s - i) {
               teamsForS += weightFreq.getOrDefault(i, 0) / 2;
            } else {
               int j = s - i;
               teamsForS += Math.min(weightFreq.getOrDefault(i, 0), weightFreq.getOrDefault(j, 0));
            }
         }
         maxTeams = Math.max(maxTeams, teamsForS);
      }
      
      System.out.println(maxTeams);
      sc.close();
   }
}
```