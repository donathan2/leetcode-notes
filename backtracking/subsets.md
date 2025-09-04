# LeetCode 78: Subsets (Medium)
### Problem Description:

Given an integer array nums of unique elements, return all possible subsets (the power set).

The solution set must not contain duplicate subsets. Return the solution in any order.

### Approach:

**Time complexity: O(n * 2^n)**

**Space complexity: O(n * 2^n)**

We want to return the power set of the given array. We can think of having a choice at every integer, whether to include it in or subarray or now. For each of those choices, we branch
off and populate that local subarray, and continuously make that decision for the rest of the integers in the array. With this, we form a graph that can lead us to every possible
subarray. To simulate this in code, we can append each integer to a local subarray and call our recursive DFS function to model including that integer in the path. To do the opposite,
we can immediately pop the integer we just appended, and then call the DFS function again to backtrack and go on with the rest of our recursion with that integer not included. 

We know the subarray is completed once the index exceeds the bounds of our array, and we can then append that to our answer.


``` python
    def subsets(self, nums: List[int]) -> List[List[int]]:
        ans = []

        subset = []

        def dfs(index):
            if index >= len(nums):
                ans.append(subset.copy())
                return

            subset.append(nums[index])
            dfs(index + 1)

            subset.pop()
            dfs(index + 1)
        
        dfs(0)

        return ans

```
