# LeetCode 138: Copy List with Random Pointer (Medium)
### Problem Description:

A linked list of length n is given such that each node contains an additional random pointer, which could point to any node in the list, or null.
Construct a deep copy of the list. 

### Approach:

**Time complexity: O(n)**

**Space complexity: O(n)**

The difficulty with this problem is determining how to manage references of nodes, as each node not only has a next pointer but a random pointer.
If we wanted to handle this in one iteration, we could theoretically create a node for every node in the chain and connect them through .next.
However, since every node has a .random pointer, if we constructed a node for every .random reference, we'd lose access to the nodein the
future and/or have duplicates of old nodes, and that just doesn't work.

If we utilize a hashmap, mapping new nodes to every original node, this problem becomes much more manageable. We simply create a copy of every node
and place it in a dictionary in one pass, and in the next pass we assign the next and random pointers based on the references we accumulated
through our dictionary. 


``` python
def copyRandomList(self, head: 'Optional[Node]') -> 'Optional[Node]':
        curr = head
        nodeMap = {}
        nodeMap[None] = None
        while (curr):
            nodeMap[curr] = Node(curr.val)
            curr = curr.next
        
        curr2 = head
        while (curr2):
            nodeMap[curr2].next = nodeMap[curr2.next]
            nodeMap[curr2].random = nodeMap[curr2.random]
            curr2 = curr2.next
        
        return nodeMap[head]

```
