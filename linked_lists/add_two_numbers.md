# LeetCode 2: Add Two Numbers (Medium)
### Problem Description:

You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list. 

### Approach:

**Time complexity: O(m + n)**

**Space complexity: O(1)**

This problem simulates the process of adding large numbers on paper. Since the digits of the number are given through reversed linked lists,
this works in our favor because we already traditionally add from right to left on paper. It isn't as simple as that however, as we need a system to manage totals
going over 10, and a system to handle extra digits as the linked lists aren't guaranteed to be the same size.

For the former, we can create a carry variable that simply tracks the amount to carry over to the next addition. If the previous sum exceeded
9, we set carry to 1 and add that to the next sum. The carry of the final sum should be added onto the end as well to simulate real addition.

If one linked list finishes before the other, we can simply bring the rest of the numbers from the other down, including any carries 
from previous summations.

My implementation of these 2 cases definitely could have been executed more gracefully, and even potentially done in one while loop, but regardless it accomplishes
the specification within the given constraints.


``` python
def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        curr1, curr2 = l1, l2
        carry = 0
        prev = head = None
        while (curr1 and curr2):
            total = curr1.val + curr2.val + carry
            carry = 1 if total >= 10 else 0
            total = total - (10 * carry)
            newNode = ListNode(total)
            if (not head):
                head = newNode
            if (prev):
                prev.next = newNode
            prev = newNode
            curr1 = curr1.next
            curr2 = curr2.next
        if (curr1 or curr2):
            remaining = curr2 if curr2 else curr1
            while (remaining):
                total = remaining.val + carry
                carry = 1 if total >= 10 else 0
                total = total - (10 * carry)
                newNode = ListNode(total)
                prev.next = newNode
                prev = newNode
                remaining = remaining.next
        if (carry):
            remainderNode = ListNode(1)
            prev.next = remainderNode
        return head

```
