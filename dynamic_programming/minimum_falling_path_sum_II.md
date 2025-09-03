# LeetCode 104: Minimum Falling Path Sum II (Hard)
### Problem Description:

Given an n x n integer matrix grid, return the minimum sum of a falling path with non-zero shifts.

A falling path with non-zero shifts is a choice of exactly one element from each row of grid such that no two elements chosen in adjacent rows are in the same column.

### Approach:

**Time complexity: O(n^2)**

**Space complexity: O(n)**

There's a really simple, greedy approach to this problem that yields the correct answer most, but not all the time. For every row, we can simply choose the lowest tile to add to our
"solution path". If the lowest tile is unable to be chosen (because it was in the same column as the chosen tile in the last row), we select the second lowest tile instead. This is 
a CRAZY fast solution of O(n). However it doesn't consider outcomes where selecting certain locally optimal tiles blocks other tiles that would lead to a more globally optimal solution.
In this case, we need to look towards a dynamic programming approach instead. 

Instead of just choosing the lowest tile every time, we can maintain a running "minimum path value" total for each tile. This means that we would store the minumum value possible we've
found that can optimally get us to a certain tile with minimum path value, in that tile. For every row, we would look at the above row (with their minimum path values), and look at the 
lowest value tile there, or if that tile is unavailable from being in the same column, we look at the second lowest value tile instead. We add that value to our current tile, and that 
becomes the current tile's minimum path value to get to that tile. Keep doing this until we make it to the bottom row, and simply return the minimum value of that row. 

We can optimize this further by only keeping storage of the previous and current rows rather than a dictionary of all the rows, as in a greedy sense, once we iterate over the 3rd row,
we won't need to retrieve any information directly from it for the 5th row and beyond. Thus, we can maintain pointers to arrays that represent out previous and current rows, the current
rows would need the previous row just to add their minimum value tile onto the current row's tiles. 

``` python
def minFallingPathSum(self, grid):
        """
        :type grid: List[List[int]]
        :rtype: int
        """

        n = len(grid)

        prev = grid[0][:]

        for row in range(1, n):
            rowMin = (-1, float("inf"))
            secMin = (-1, float("inf"))
            for col in range(n):
                curTile = (col, prev[col])
                if curTile[1] < rowMin[1]:
                    rowMin, secMin = curTile, rowMin
                elif curTile[1] < secMin[1]:
                    secMin = curTile

            newRow = [0] * n
            for col in range(n):
                if col == rowMin[0]:
                    newRow[col] = grid[row][col] + secMin[1]
                else:
                    newRow[col] = grid[row][col] + rowMin[1]

            prev = newRow

        return min(prev)

```
