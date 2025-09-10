# LeetCode 212: Word Search II (Hard)
### Problem Description:

Given an m x n board of characters and a list of strings words, return all words on the board.

Each word must be constructed from letters of sequentially adjacent cells, where adjacent cells are horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

### Approach:

**Time complexity: O(m * n * 4 * (3^(t-1)) + s)**

**Space complexity: O(s) (sum of lengths of words)**

This problem combines a lot of programming elements from different categories. At its core, I'd say it's a backtracking and Trie problem, but
it uses the same grid traversal algorithm from other graph problems. We could use the same algorithm from Word Search I and apply it to
all the words we're given, but that could be extremely costly since we could have up to 3 * 10^4 words, and we'd have to iterate through
each of those words with every tile check.

Thus, we can use a trie instead. Whereas before we check if a grid tile contains the next sequential letter in a word, we can just check
if a grid tile is the child of the trie node we're traversing. if we reach a trie node whose wordEnd field is not None, we know we've reached
the end of the word and can append it to our answer list. This makes checking for all of our words much more efficient. 

For a brief algorithmic summary, I first populate a trie of all of my words. Then, I iterate through the tiles of the grid. If any of those 
grids carry a letter in my root's children, this signifies it could be the start of one of the word's I'm looking for. Thus, I begin DFS on 
it. I recursively look at all of the tiles adjacent to my current tile and see if they continue the word (by being children in my current 
trie). Every tile I traverse is placed into a visited set tied to the initial dfs call, but then removed from the set after the dfs call
closes, as they need to be traversable again outside of their specific dfs call. Once a node I traverse has a wordEnd field not equal to 
None, I add that word to the ans array. I return that array after iteration concludes.

``` python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.wordEnd = None

class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        root = TrieNode()

        found = set()
        ans = []

        directions = [(1, 0), (-1, 0), (0, 1), (0, -1)]

        for word in words:
            curr = root
            for ch in word:
                if ch not in curr.children:
                    curr.children[ch] = TrieNode()
                curr = curr.children[ch]
            curr.wordEnd = word


        def dfs(row, col, node, visited):
            if node.wordEnd and node.wordEnd not in found:
                found.add(node.wordEnd)
                ans.append(node.wordEnd)
            for dy, dx in directions:
                ny, nx = dy + row, dx + col
                if 0 <= ny < len(board) and 0 <= nx < len(board[0]) and board[ny][nx] in node.children and (ny, nx) not in visited:
                    visited.add((ny, nx))
                    dfs(ny, nx, node.children[board[ny][nx]], visited)
                    visited.remove((ny, nx))

        
        for row in range(len(board)):
            for col in range(len(board[0])):
                if board[row][col] in root.children:
                    visited = set([(row, col)])
                    dfs(row, col, root.children[board[row][col]], visited)

        return ans

            


        

```
