# LeetCode 141: Linked List Cycle (Easy)
### Problem Description:

Identify whether a given linked list contains a cycle or not.

### Approach:

**Time complexity: O(n)**

**Space complexity: O(1)**

The key to this problem is slow and fast pointers. Utilizing a slow pointer that travels 1 node per iteration and a fast pointer that 
travels 2 nodes per iteration, we guarantee that at some point both pointers will point to the same node if there's a cycle in the linked
list (and thus return true). There's a proof for this based on modular arithmetic and the pigeonhole principle, but for this problem we really just need to understand
that it works. 

If there isn't a cycle, fast will always reach the end of the list first. Thus, we track if fast or fast.next ever equals None, and return
false in that case.


``` python
    def hasCycle(self, head):
        """
        :type head: ListNode
        :rtype: bool
        """
        slow = fast = head

        while fast and fast.next:
            fast = fast.next.next
            
            slow = slow.next

            if (fast == slow):
                return True
        return False

```
