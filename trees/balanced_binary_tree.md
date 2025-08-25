# LeetCode 110: Balanced Binary Tree (Easy)
### Problem Description:

Given a binary tree, determine if it is height-balanced.

### Approach:

**Time complexity: O(n)**

**Space complexity: O(n)**

With this problem we're building on the fundamentals of binary tree depth. The idea here is that for any node, if the absolute value of
the left child depth minus the right child depth exceeds 1, we know that the this isn't a balanced binary tree. We can employ this
recursively and do a DFS search to find nodes that fit this description. We then have global variable that ticks false whenever we have 
a node that we know confirms the tree isn't balanced. 


``` python
def isBalanced(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: bool
        """
        self.balanced = True
        self.traverse(root)
        return self.balanced


def traverse(self, root):
        if (not root):
            return 0
        leftDepth = (1 + self.traverse(root.left))
        rightDepth = (1 + self.traverse(root.right))

        if (abs(leftDepth - rightDepth) > 1):
            self.balanced = False
                
        return max(leftDepth, rightDepth)

```
