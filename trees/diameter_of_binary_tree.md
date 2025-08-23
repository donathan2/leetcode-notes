# LeetCode 543: Diameter of Binary Tree (Easy)
### Problem Description:

Given the root of a binary tree, return the length of the diameter of the tree.

### Approach:

**Time complexity: O(n)**

**Space complexity: O(n)**

This problem seems a bit tough at first as the diameter itself could be anywhere theoretically. It doesn't have to go through the
original tree's root, so we need to carefully think about how to approach the problem. Any diameter will come from a root of some kind, thus we can 
calculate the individual diameters for every node, where that node is the root to test. 

First, we can set a global variable that tracks our current highest diameter that updates when exceeded. Then, we can utilize a recursive 
algorithm that calculates max left and right depth for every node, which added together make up the diameter of that subtree. We compare this with the
out global diameter variable, and continue to do this with every node in the tree. For every function call, we return the maximum of the 
left depth and right depth, as this will represent the left/right depth (depending on this node's position) of its parent. 


``` python
def diameterOfBinaryTree(self, root):
        """
        :type root: Optional[TreeNode]
        :rtype: int
        """
        self.maxDiameter = 0
        self.search(root)
        return self.maxDiameter


    def search(self, root):
        leftDepth = (1 + self.search(root.left)) if root.left else 0
        rightDepth = (1 + self.search(root.right)) if root.right else 0

        localDepth = leftDepth + rightDepth
        self.maxDiameter = max(self.maxDiameter, localDepth)

        return max(leftDepth, rightDepth)

```
