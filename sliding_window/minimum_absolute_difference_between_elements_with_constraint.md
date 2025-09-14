# LeetCode 2817: Minimum Absolute Difference Between Elements With Constraint (Medium)
### Problem Description:

You are given a 0-indexed integer array nums and an integer x.

Find the minimum absolute difference between two elements in the array that are at least x indices apart.

In other words, find two indices i and j such that abs(i - j) >= x and abs(nums[i] - nums[j]) is minimized.

Return an integer denoting the minimum absolute difference between two elements that are at least x indices apart.

### Approach:

**Time complexity: O(nlogn)**

**Space complexity: O(n)**

This problem would be incredibly simple to solve with its brute force solution. For every num in nums, we'd iterate through nums and find their difference if their positional difference
was at least x. However, this is o(n^2) and way too slow, so we instead have to rely on another quicker algorithm.

We can do a binary search/greedy/sliding window kind of algorithm. Keep track of two pointers, a left and a right. We start right at x and left at 0, and the idea is that every value 
in nums with index left or lower is an eligible "min-pairing" for nums[right], as they are at least x indices apart.. We will iterate through nums until right reaches the end, 
incrementing left and right gradually. Every left will be added via  bisect.insort into a sorted array we maintain. We can then find the appropriate sorted position of right in the 
array with bisect.bisect, and check its neighbors for distances. This works as every value in the array is guaranteed to be an eligible pairing with the current value at right, and the 
neighbors of that value are guaranteed to be the 2 best options as they would be the most similar in value and thus the lowest in difference. As we iterate, we keep track of the 
global min difference, and return it at the end.

``` python
    class Solution(object):
    def minAbsoluteDifference(self, nums, x):
        """
        :type nums: List[int]
        :type x: int
        :rtype: int
        """
        sortedList = []
        l, r = 0, x
        minDif = float("inf")

        while r < len(nums):
            bisect.insort(sortedList, nums[l])
            pos = bisect.bisect(sortedList, nums[r])
            leftVal = float("inf") if pos == 0 else sortedList[pos - 1]
            rightVal = float("inf") if pos == len(sortedList) else sortedList[pos]

            minDif = min(minDif, abs(leftVal - nums[r]), abs(rightVal - nums[r]))
            l += 1
            r += 1
        return minDif

```
