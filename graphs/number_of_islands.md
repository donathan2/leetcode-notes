# LeetCode 200: Number of Islands (Medium)
### Problem Description:

Given an m x n 2D binary grid grid which represents a map of '1's (land) and '0's (water), return the number of islands.

An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

### Approach:

**Time complexity: O(m * n) (rows * columns)**

**Space complexity: O(m * n) (rows * columns)**

The key to this problem is BFS. We'll keep a set of coordinates we've already traversed (and thus know belong to an island already), and then iterate through the tiles of the grid.
Once we come across a tile that isn't in the set, we know we've come across a "new island" and can increment our island counter, then run BFS on the tile. We'll add the tile to a 
deque and continuously popleft and add the adjacent tiles that are 1) land, and 2) not in the coordinate set. Eventually we'll reach all the tiles in the island and they will become
part of the set. Once the deque is empty, we know we've cleared the island. After iterating through the grid, we'll return island counter.


``` python
    class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        visited = set()
        islandCount = 0

        directions = [(0, 1), (0, -1), (1, 0), (-1, 0)]

        def bfs(row, col):
            knownLand = deque([(row,col)])
            while knownLand:
                newLand = knownLand.popleft()
                for y, x in directions:
                    newY = y + newLand[0]
                    newX = x + newLand[1]
                    if 0 <= newY < len(grid) and 0 <= newX < len(grid[0]) and grid[newY][newX] == '1' and ((newY, newX) not in visited):
                        knownLand.append((newY, newX))
                        visited.add((newY, newX))

        for row in range(len(grid)):
            for col in range(len(grid[0])):
                if grid[row][col] == '1' and (row, col) not in visited:
                    islandCount += 1
                    bfs(row, col)
                    visited.add((row, col))
        return islandCount


```
