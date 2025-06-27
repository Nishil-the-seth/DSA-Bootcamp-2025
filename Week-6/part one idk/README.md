# Dynamic Programming

## What is dynamic programming?
Dynamic Programming is a commonly used algorithmic technique used to optimize recursive solutions when same subproblems are called again.

* The core idea behind DP is to store solutions to subproblems so that each is solved only once.
* To solve DP problems, we first write a recursive solution in a way that there are overlapping subproblems in the recursion tree (the recursive function is called with the same parameters multiple times)
* To make sure that a recursive value is computed only once (to improve time taken by algorithm), we store results of the recursive calls.
* There are two ways to store the results, one is top down (or memoization) and other is bottom up (or tabulation).

---

## When to use DP?

Dynamic programming is used for solving problems that consists of the following characteristics:
1. **Optimal Substructure**
   
   This property means that we use the optimal results of subproblems to achieve the optimal result of the bigger problem.

2. **Overlapping Subproblems**

   The same subproblems are solved repeatedly in different parts of the problem refer to Overlapping Subproblems Property in Dynamic Programming.
