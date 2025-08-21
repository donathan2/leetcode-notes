# LeetCode 143: Reorder List (Medium)
### Problem Description:

Reorder a given linked list to order of [0, n-1, 1, n-2, 2, n-3, ...]

### Approach:

**Time complexity: O(n)**

**Space complexity: O(1)**

This problem comes across really awkward at first just because of how weird the desired return order is. It's kind of like an inwards ping-pong
back and forth. I noticed however that if I reversed the second half of the list, all I simply had to do was alternate between the heads of the
first and second halves of the list to get it into the correct order. 

To reverse the second half of the list, I used slow and fast pointers to find the middle (stopping when fast reached none), as linked lists 
dont support length or indexing. I recorded the end of the "slow" list, and used that to identify the start of the "fast" list. From here,
I just needed to reverse the second half of the list using a common iteration algorithm. Then, I kept respective pointers and alternated between
the heads of the two lists and connected them. This was actually a little bit awkward, as I not only had to maintain pointers for the next node
in a given list, but also the next node to connect to in the other list. Regardless, it's still an O(n) time and O(1) solution.

``` python
def reorderList(self, head: Optional[ListNode]) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        if not head or not head.next:
            return
            
        slow = fast = firstEnd = head
        while (fast and fast.next):
            firstEnd = slow
            slow = slow.next
            fast = fast.next.next
        firstEnd.next = None
        secondList = slow

        curr = secondList
        prev = None
        while curr:
            nxt = curr.next
            curr.next = prev
            prev = curr
            curr = nxt

     
        curr = head
        other = prev
        nxt = curr.next

        while (curr and other):
            curr.next = other
            curr = curr.next

            other = nxt
            nxt = curr.next

```
