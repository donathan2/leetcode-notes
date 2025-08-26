# LeetCode 572: Subtree of Another Tree (Easy)
### Problem Description:

Given the roots of two binary trees root and subRoot, return true if there is a subtree of root with the same structure and node values of subRoot and false otherwise.

### Approach:

**Time complexity: O(m * n)**

**Space complexity: O(m + n)**

This question builds on LeetCode 100 (Same Tree), except this time this subtree could be located anywhere in our other tree. An option we
have is to recursively cycle through the nodes of our tree until we find a node with a value that matches out subtree's root value. When we 
do find one, we can implement a similar algorithim to LeetCode 100 and continuously compare the rest of the nodes in both trees 
recursively to ensure their equality. Once all recursive calls reach non-existant nodes, that tells us the entire subtree was in the tree
and we can return True. 



``` python
def isSubtree(self, root, subRoot):
        """
        :type root: Optional[TreeNode]
        :type subRoot: Optional[TreeNode]
        :rtype: bool
        """
        if not subRoot:
            return True
        if not root:
            return False
        if self.traverse(root, subRoot):
            return True
        return self.isSubtree(root.left, subRoot) or self.isSubtree(root.right, subRoot)
        
def traverse(self, root, subRoot):
        if not root and not subRoot:
            return True
        elif (root and subRoot and root.val == subRoot.val):
            return self.traverse(root.left, subRoot.left) and self.traverse(root.right, subRoot.right)
        else:
            return False

```
