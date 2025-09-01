# LeetCode 2672: Number of Adjacent Colors With the Same Color (Medium)
### Problem Description:

You are given an integer n representing an array colors of length n where all elements are set to 0's meaning uncolored. You are also given a 2D integer array queries where queries[i] = [indexi, colori]. For the ith query:

Set colors[indexi)] to colori.
Count the number of adjacent pairs in colors which have the same color (regardless of colori).
Return an array answer of the same length as queries where answer[i] is the answer to the ith query.



### Approach:

**Time complexity: O(q) (length of queries)**

**Space complexity: O(n + q) (length of queries + colors)**

This problem is more confusing than anything else. Queries tells us how to transform the colors array, and with every ith query, the ith index of our return array should be the
amount of adjacent colors there currently were. The key to this problem is that every query can only update up to two pairs, the index to the left and right. After updating the 
color array directly, we should check if the left and right exist. If they do, we simply compare them to the original and new colors of that index. If originally they were the same, 
subtract 1 from our adjacency count, or if now they are the same, we add 1 to the adjacency count. 

In the case that the element we're changing was already 0 (uncolored), I treat the original color as equal to -1 as 0s adjacent to other 0ss don't count as an adjacent color pair and 
thus shouldn't increment the adjacency counter.


``` python
def colorTheArray(self, n, queries):
        """
        :type n: int
        :type queries: List[List[int]]
        :rtype: List[int]
        """

        adj = 0
        ans = []
        colors = [0] * n
        for query in queries:
            ogColor = colors[query[0]] if colors[query[0]] != 0 else -1
            colors[query[0]] = query[1]

            if  query[0] > 0:
                left = colors[query[0] - 1] 
            else:
                left = None
            if query[0] < n - 1:
                right = colors[query[0] + 1]
            else:
                right = None

            if ogColor == left:
                adj -=1
            if ogColor == right:
                adj -=1
            if query[1] == left:
                adj +=1
            if query[1] == right:
                adj +=1

            ans.append(adj)
            
        return ans

```
