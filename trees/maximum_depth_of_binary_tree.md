# LeetCode 104: Maximum Depth of Binary Tree (Easy)
### Problem Description:

Given the root of a binary tree, return its maximum depth.

### Approach:

**Time complexity: O(n)**

**Space complexity: O(n)**

We can use a recursive algorithm to find the maximum depth of the tree. With each function call, we return 0 if the node doesn't exist, 
or 1 + the call of the remaining node chain. We need to be careful however, as we only want to return a number representing the maximum depth, not 
the total amount of nodes in the tree. Thus we use the max() function to ensure we're only returning the maximum depth.


``` python
def maxDepth(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: int
        """
        if (not root):
            return 0
        else:
            return max(1 + self.maxDepth(root.left), 1 + self.maxDepth(root.right))

```
