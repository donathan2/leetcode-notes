# LeetCode 621: Task Scheduler (Medium)
### Problem Description:

You are given an array of CPU tasks, each labeled with a letter from A to Z, and a number n. Each CPU interval can be idle or allow the completion of one task. Tasks can be completed in any order, but there's a constraint: there has to be a gap of at least n intervals between two tasks with the same label.

Return the minimum number of CPU intervals required to complete all tasks.

### Approach:

**Time complexity: O(n)**

**Space complexity: O(1) (Technically since we have a max of 26 characters)**

Our approach to this problem will revolve around 1 core greedy algorithm; the next task to handle will always be the one with the highest
frequency, or one of the ones with the highest frequency. Prioritizing tasks with lower frequency will lead to excess remaining tasks of one 
character being left over, and thus we would need to spend extra time on idle intervals which is nonoptimal. 

We will make use of various data structures. We want a max heap that will tell us which kind of task should be done next, and since this
is dependent on the counts of each task type, we need a hashmap to effectively count all the types to add them to the max heap. Then, once
in the max heap, we will continuously pop the highest frequency task. (Since Python implements heaps as min heaps, we will add our values
as negative to simulate it as a max heap) Once popped, if our task hasn't hit frequency 0 yet, it needs somewhere to go to indicate it's on
cooldown and can't be popped again until its cooldown is up. We can use a deque for this, as it allows for O(1) left end popping. With 
every max heap pop, we will check if the task at the left end's cooldown is up. We do this by having a running time counter that increments
with every max heap / deque pop cycle. 

This process is over once our max heap and deque are empty. We return the count on the running timer afterwards.




``` python
    def leastInterval(self, tasks, n):
        """
        :type tasks: List[str]
        :type n: int
        :rtype: int
        """
        charCount = {}
        charHeap = []
        charQueue = deque()
        for x in tasks:
            charCount[x] = charCount.get(x,0) + 1
        
        for x in charCount.values():
            heapq.heappush(charHeap, -x)
        

        intervals = 0
        while charHeap or charQueue:
            intervals += 1
            if charHeap:
                nextTask = heapq.heappop(charHeap)
                if nextTask + 1 != 0:
                    charQueue.append((nextTask + 1, intervals + n))
            if charQueue and charQueue[0][1] == intervals:
                heapq.heappush(charHeap, charQueue.popleft()[0])
        return intervals

```
