# LeetCode 100: Same Tree (Easy)
### Problem Description:

Given the roots of two binary trees p and q, write a function to check if they are the same or not.

### Approach:

**Time complexity: O(n)**

**Space complexity: O(n)**

This question is relatively simple as we only have to compare what would be the respective nodes from p and q. We can do this simply with a
recursive algorithm that checks if their two nodes are the same, and if not we can instantly return False. In cases where p and q don't exist,
that means we've reached the end of a node chain and can return True, but if only one doesn't exist, we instantly return False as p and
q should always be either the same or not the same. We check that both the left and right sides of our root return True before we return True. 


``` python
def isSameTree(self, p, q):
        """
        :type p: Optional[TreeNode]
        :type q: Optional[TreeNode]
        :rtype: bool
        """
        if not p and not q:
            return True
        if not p or not q:
            return False
        if p.val != q.val:
            return False


        return self.isSameTree(p.left, q.left) and self.isSameTree(p.right, q.right)

```
