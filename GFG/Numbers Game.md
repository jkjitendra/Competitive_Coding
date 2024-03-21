# Numbers Game:

## Problem Statement:

Geek is appearing for a coding contest. The aim of the contest is to score **exactly N points.** He is given an **integer k**, before the start of the contest.

For **each problem he solves** during the contest, he is asked to choose an integer m, and m `<sup>`k `</sup>` **is added to his score**.

Help Geek find the **minimum number of problems** he must solve to achieve **exactly N points.**

**Note:** For each different problem, he can choose different values of **m** but the value of **k** is same for all problems

#### Example 1:

```
Input: 
N = 12
k = 2

Output: 3

Explanation: He can solve three problems, and choose m = 2 for all of them. Hence, 2^2 + 2^2 + 2^2 = 12. 
```

#### Example 2:

```
Input:

N=13
k=2

Output: 2

Explanation: He can solve two problems, and choose m=3 for one, and m=2 for the second problem. Hence 3^2 + 2^2 = 13.
```

#### Your Task:

This is a function problem. The input is already taken care of by the driver code. You only need to complete the function score() that takes an integer N and integer k as input arguments. Return an integer denoting the minimum number of problems Geek needs to solve. The driver code takes care of the printing.

#### Constraints:

- 1<=N<=20000
- 1<=K<=29

## Solution:

#### Method 1:

```java

```