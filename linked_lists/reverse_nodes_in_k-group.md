# LeetCode 25: Reverse Nodes in k-Group (Hard)
### Problem Description:

Given the head of a linked list, reverse the nodes of the list k at a time, and return the modified list.

### Approach:

**Time complexity: O(n)**

**Space complexity: O(1)**

This problem is relatively simple as at its core it's just asking for repeated linked list reversals. The only real tricky thing is rehooking
the nodes back up, but we can accomplish this through initializing variables for certain nodes we know will be the start/end of a reversal
chain. In my solution I used left and right pointers to find the beginning and end of a linked list segment to reverse. Once the right pointer
reached the end of the linked list, the process stopped and I instantly returned the linked list in its given form.

This problem can get tricky managing all the pointers to nodes that have been reversed and previously iterated over, but at its core there
really aren't any out of the box or complex programming ideas here. 


``` python
class Solution(object):
    def reverseKGroup(self, head, k):
        """
        :type head: Optional[ListNode]
        :type k: int
        :rtype: Optional[ListNode]
        """
        firstIte = True
        lastChain = prev = newHead = None
        curr = left = right = head

        while True:
            left = right = curr
            for x in range(k - 1):
                if (right):  
                    right = right.next     
            if (not right):
                if (lastChain):
                    lastChain.next = left
                    return newHead
            else:
                tempChainStart = curr
                counter = 1
                while (counter <= k):
                    nextNode = curr.next
                    curr.next = prev
                    prev = curr
                    curr = nextNode
                    counter += 1
                if (firstIte):
                    newHead = prev
                    firstIte = False
                if (lastChain):
                    lastChain.next = prev
                lastChain = tempChainStart

```
