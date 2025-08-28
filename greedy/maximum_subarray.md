# LeetCode 53: Maximum Subarray (Medium)
### Problem Description:

Given an integer array nums, find the subarray with the largest sum, and return its sum.

### Approach:

**Time complexity: O(n)**

**Space complexity: O(1)**

This problem seems simple with a lot of open-ended approaches, but Kadane's algorithm is the best for this as it has O(n) time complexity with constant space. Essentially, we're just 
going to do one simple iterative pass through the array. For every value, we add it and keep a running sum in some kind of current sum variable, while also tracking our global maximum
sum in another variable. The greedy approach comes in for how we handle negative sums. If a negative number decreases the current sum to a negative value, we know it won't be worth it
any more to continue keeping track of the current subarray we're measuring, as it will only "weigh down" future values. Thus, we can just reset our current sum to 0 to simulate 
starting the subarray anew with the next value. 

This is a greedy approach because we're making a local optimization with every value to either continue the subarray or restart it based on
its total sum. Usually greedy approaches aren't optimal, but this one happens to be so. 


``` python
    def maxSubArray(self, nums):
        """
        :type nums: List[int]
        :rtype: int
        """
        maxSum, currSum = nums[0], 0
        for num in nums:
            if currSum < 0:
                currSum = 0
            currSum += num
            maxSum = max(currSum, maxSum)
        return maxSum

```
