# LeetCode 206: Reverse Linked List (Easy)
### Problem Description:

Reverse a linked list!

### Approach:

**Time complexity: O(n)**

**Space complexity: O(1)**

To reverse the linked list, my plan was to iterate through the list, and simply reverse the next pointer 
for each node as I traversed. However, this could get tricky as in order to "reverse" a node, I'd have to
change its next pointer, meaning I wouldn't be able to iterate through to the next node directly. Thus, I
had to maintain some pointers as I iterated through:

- curr: the current Node
- prev: the previous Node
- nextNode: the next Node to iterate to

From here, I had everything I needed to reverse the linked list. With each iteration, I'd first update the nextNode, 
then I could reassign the curr.next to the previous node, then assign prev to the current node to ensure it's hooked
up for the next iteration.

Note: for the first iteration, I'd have to assign first assign prev to None and curr to head as these variables don't have proper values yet.

``` python
def reverseList(self, head):
        """
        :type head: ListNode
        :rtype: ListNode
        """
        prev = None
        curr = head
        while (curr):
            nextNode = curr.next
            curr.next = prev
            prev = curr
            curr = nextNode
        return prev

```




