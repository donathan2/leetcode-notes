# LeetCode 21: Merge Two Sorted Lists (Easy)
### Problem Description:

Given two sorted lists, merge them into one list of non-decreasing order!

### Approach:

**Time complexity: O(n + m)**

**Space complexity: O(1)**

Given that both lists are sorted, we know the next node of our sorted list will always be one of the next nodes from one of the lists.
Thus, we can simply iterate through and compare the next nodes from both lists, and attach the lower one. To ensure simplicity, we can first add references to
"starter nodes" that we won't actually return. This makes initializing the process a lot simpler, as we won't need to add additional code
to find the beginning of the list. 

We stop iterating once we've hit the end of either one of the lists. Then, we add the final node of the list that wasn't completed. We do this
as we can't compare nodes with values of Non, so we do this to be extra safe.


``` python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution(object):
    def mergeTwoLists(self, list1, list2):
        """
        :type list1: Optional[ListNode]
        :type list2: Optional[ListNode]
        :rtype: Optional[ListNode]
        """

        start = node = ListNode()
        
        while (list1 and list2):
            if (list1.val < list2.val):
                node.next = list1
                list1 = list1.next
            else:
                node.next = list2
                list2 = list2.next
            node = node.next
        if (list2):
            node.next = list2
        else:
            node.next = list1
        
        return start.next

```
