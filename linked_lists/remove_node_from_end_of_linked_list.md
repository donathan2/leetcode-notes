# LeetCode 19: Remove Nth Node From End of List (Medium)
### Problem Description:

Given a linked list and an integer n, remove the nth node from the end of the list.

### Approach:

**Time complexity: O(n)**

**Space complexity: O(1)**

This problem is kind of weird at first because we don't have any ways to directly identify the end of a linked list, so it can be puzzling
to figure out how to access the nth node from the end. However, we can set up two pointers that help us do that, a left and a right. We move
the right pointer along n nodes, then we iteratively progress both pointers until right reaches the end. Since right is n nodes ahead of left,
left should now be at the node to remove. For ease, I stopped the iteration when right.next was None, as then left would stop at the node just
before the nth node from the right, and thus would make rehooking up the nodes easier. From here, we can just set left.next to left.next.next.

There's also the case where iteration doesn't happen at all, as n is equal to the length of the list and left is None. Calling left.next here
would create an error, so in this case I instantly return left.next, as this returns the rest of the list safely.

``` python
def removeNthFromEnd(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        left = right = head

        for x in range(n):
            right = right.next
        
        if (not right):
            return left.next
        
        while (right.next):
            left = left.next
            right = right.next
        left.next = left.next.next

        return head

```
