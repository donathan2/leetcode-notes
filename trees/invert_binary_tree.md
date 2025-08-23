# LeetCode 226: Invert Binary Tree (Easy)
### Problem Description:

Given the root of a binary tree, invert the tree, and return its root.

### Approach:

**Time complexity: O(n)**

**Space complexity: O(n)**

We can employ a divide and conquer algorithm here. With any given node, its left and right children should be swapped. We do this, and then apply the same recursive code to both of its children.
We stop this process once a node doesn't exist, indicating that we've reached the bottom of the node chain and have successfully inverted all of the above nodes.


``` python
def invertTree(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: Optional[TreeNode]
        """
        if (not root):
            return None
        
        left = root.left
        root.left = root.right
        root.right = left

        self.invertTree(root.left)
        self.invertTree(root.right)

        return root

```
