# Climbing Stairs Problem

There are n stairs, and a person standing at the bottom wants to climb stairs to reach the top. The person can climb either 1 stair or 2 stairs at a time, the task is to count the number of ways that a person can reach at the top.

There are multiple ways to solve this problem in varying levels of complexity. 

---

## Using Memoization
**Time complexity:** O(n)  
**Space complexity:** O(n)  
Number of ways to reach the nth stair, i.e., countWays(n), depends on the optimal solutions of the subproblems countWays(n-1) and countWays(n-2). By combining these optimal substructures, we can efficiently calculate the total number of ways to reach the nth stair.


## Using Tabulation
**Time complexity:** O(n)  
**Space complexity:** O(n)

## Using Space Optimized DP
**Time complexity:** O(n)  
**Space complexity:** O(1)

## Using Matrix Exponentiation
**Time complexity:** O(logn)  
**Space complexity:** O(1)
