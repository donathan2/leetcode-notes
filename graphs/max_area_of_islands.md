# LeetCode 695: Max Area of Island (Medium)
### Problem Description:

You are given an m x n binary matrix grid. An island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

The area of an island is the number of cells with a value 1 in the island.

Return the maximum area of an island in grid. If there is no island, return 0.

### Approach:

**Time complexity: O(m * n) (rows * columns)**

**Space complexity: O(m * n) (rows * columns)**

This problem is very similar to Number of Islands (LeetCode 200). We'll use the same algorithm, iterating through the tiles of the grid, 
and performing BFS on any tile not in our visited set already. This time however, as we popleft through our deque, we will increment a
new counter that tracks the area of the current island. After an individual BFS call is completed, we'll return a value that represents the
area of the current island. If that value is higher than our max area counter, we'll swap it to that area. Otherwise, the algorithm 
is nearly identical. 


``` python
    class Solution:
    def maxAreaOfIsland(self, grid: List[List[int]]) -> int:
        maxArea = 0
        visited = set()

        directions = [(0, 1), (0, -1), (-1, 0), (1, 0)]

        def bfs(row, col):
            curArea = 0
            landQueue = deque([(row, col)])
            while landQueue:
                curLand = landQueue.popleft()
                curArea += 1
                for y, x in directions:
                    ny, nx = y + curLand[0], x + curLand[1]
                    if 0 <= ny < len(grid) and 0 <= nx < len(grid[0]) and grid[ny][nx] == 1 and (ny, nx) not in visited:
                        landQueue.append((ny, nx))
                        visited.add((ny, nx))
            return curArea

        for row in range(len(grid)):
            for col in range(len(grid[0])):
                if (grid[row][col] == 1 and ((row, col) not in visited)):
                    visited.add((row, col))
                    area = bfs(row, col)
                    maxArea = max(area, maxArea)
        return maxArea
```
