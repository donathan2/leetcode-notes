# LeetCode 23: Merge k Sorted Lists (Hard)
### Problem Description:

Given an array of k linked-lists lists, each linked-list sorted in ascending order, 
merge all the linked-lists into one sorted linked-list and return it.

### Approach:

**Time complexity: O(n * k)**

**Space complexity: O(1)**

This is actually a relatively simple problem and builds on merging two sorted lists. We can take the given array of linked lists, pop the last
2 lists, and merge them. We use the same process from LeetCode 21 where we iterate while both lists are still ongoing, attaching the smaller
of the two current nodes until a final list is created. For this problem, we do this, add the list back into the array, 
and continue until the array is only 1 item long, and that's out final linked list!

This satisfies the O(n * k) time complexity requirement, but there are actually heap or divide and conquer approaches that complete
this task in O(nlogk), which is faster. Regardless, this is a simple way to solve this problem and it satisfies the constraints. 




``` python
def mergeKLists(self, lists):
        """
        :type lists: List[Optional[ListNode]]
        :rtype: Optional[ListNode]
        """
        while len(lists) > 1:
            list1 = lists.pop()
            list2 = lists.pop()

            tempHead = curr = ListNode()
            while (list1 and list2):
                if list1.val < list2.val:
                    curr.next = list1
                    list1 = list1.next
                else:
                    curr.next = list2
                    list2 = list2.next
                curr = curr.next
            if (list1 or list2):
                curr.next = list1 or list2
            lists.append(tempHead.next)
        return lists[0] if len(lists) == 1 else None

```
