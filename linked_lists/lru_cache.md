# LeetCode 146: LRU Cache (Medium)
### Problem Description:

Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

### Approach:

**Time complexity: O(1) for put() and get()**

**Space complexity: O(n)**

When first approaching this problem I wasn't familiar with what a LRU cache was, but essentially it's a storage system that works 
under the philosophy that items recently accessed are more likely to be accessed again and should stay in the cache, while older 
items will be evicted. When get or put is called, the cache should "refresh" that key's priority. 

The main hurdle with this problem is the strict O(1) time complexity requirement for get and put, including the repriorities of the
keys when called. A few data structures come to mind given this, a hashmap will always reliably provide O(1) time for looking up a key's
value and adding a value to a dictionary. However, we still have the issue of how we will manage priority order and editting it upon
get and put call. While certain data structures like arrays have O(1) methods like append that could theoretically work with certain
calls, it gets increasingly complicated with reordering the cache. The only data structure that can reliably do this in O(1) time is
a linked list. Thus, for this problem we need to integerate a Node class as it's not initially given. We use these two data structures 
in tandem.

Upon get call, we check if a key is in our dictionary in O(1) time, and then re-edit the linked list to move that key to the front in 
constant time. Admittedly, my re-editting was overly complicated for this problem and could definitely be improved for clarity. However,
the data structure outlines are there and it satisfies the time and space complexity requirements.

For a put call, we have a similar process in checking the dictionary for our key to determine if we need to kick a node out, or just 
reprioritize one.


``` python
class Node:

    def __init__(self, key, val):
        self.key, self.val = key, val
        self.prev = self.next = None

class LRUCache(object):

    def __init__(self, capacity):
        """
        :type capacity: int
        """
        self.cache = {}
        self.keyChain = None
        self.capacity = capacity
        self.count = 0
        self.left = None
        self.right = None


    def get(self, key):
        """
        :type key: int
        :rtype: int
        """

        print("getting:")
        print(key)

        if (key in self.cache):
            if (self.left == self.right):
                curr = self.left
                return self.cache[key].val
            elif (self.cache[key] == self.left):
                self.left = self.left.next
                if (self.left):
                    self.left.prev = None
                self.right.next = self.cache[key]
                self.cache[key].prev = self.right
                self.right = self.cache[key]
                self.right.next = None
                curr = self.left
                return self.cache[key].val
            elif (self.cache[key] == self.right):
                curr = self.left
                return self.cache[key].val
            else:
                self.cache[key].prev.next = self.cache[key].next
                self.cache[key].next.prev = self.cache[key].prev
                self.cache[key].prev = self.right
                self.right.next = self.cache[key]
                self.right = self.cache[key]
                self.right.next = None
                curr = self.left
                return self.cache[key].val

        else:
            return -1
                

        

    def put(self, key, value):
        """
        :type key: int
        :type value: int
        :rtype: None
        """

        if (key not in self.cache):
            self.cache[key] = Node(key, value)
            self.count += 1

            if (self.right):
                
                self.right.next = self.cache[key]
                self.cache[key].prev = self.right
                self.right = self.cache[key]
                
                if self.count > self.capacity:
                    del self.cache[self.left.key]
                    self.left = self.left.next
                    self.left.prev = None
                    self.count -= 1
            else:
                self.left = self.cache[key]
                self.right = self.cache[key]
                
        else:


            if (self.left == self.right):
                self.cache[key] = Node(key,value)
                self.left = self.cache[key]
                self.right = self.cache[key]

            elif (self.cache[key] == self.left):
                if (self.left):
                    self.left.prev = None
                self.left = self.left.next
                self.cache[key] = Node(key,value)
                self.right.next = self.cache[key]
                self.cache[key].prev = self.right
                self.right = self.cache[key]

            elif (self.cache[key] == self.right):
                self.right.next = Node(key,value)
                if (self.right.prev):
                    self.right.prev.next = self.right.next
                    self.right.next.prev = self.right.prev
                self.cache[key] = self.right.next
                self.right = self.cache[key]
            else:
                self.cache[key].prev.next = self.cache[key].next
                self.cache[key].next.prev = self.cache[key].prev
                self.cache[key] = Node(key, value)
                self.cache[key].prev = self.right
                self.right.next = self.cache[key]
                self.right = self.cache[key]
        curr = self.left

```
