# LeetCode 211: Design Add and Search Words Data Structure (Medium)
### Problem Description:

Design a data structure that supports adding new words and finding if a string matches any previously added string.

Implement the WordDictionary class:

WordDictionary() Initializes the object.

void addWord(word) Adds word to the data structure, it can be matched later.

bool search(word) Returns true if there is any string in the data structure that matches word or false otherwise. word may contain dots '.' where dots can be matched with any letter.


### Approach:

**Time complexity: O(n)**

**Space complexity: O(t + n) (length of string and node count)**

This is almost identical to the original implement trie problem (LeetCode 208), but this one's addition of the "." character makes the 
search method a bit more complicated. For every "." we come across, we want to recursively traverse the current node's children, and see if
any of their paths satisfy the rest of the word. We can do this with another function defined within, passing in the node, and either the
remainder of the word (using string slicing), or passing the index of the character we're trying to check. The index approach saves a lot of
time as string slicing takes up to O(n) for every slice, so I opted for that. If any of those paths fit the rest of the word, we return true.
The rest of the implementation (for addWord) is basically identical to the original implement trie problem.

``` python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.endWord = False

class WordDictionary:

    def __init__(self):
        self.root = TrieNode()
        

    def addWord(self, word: str) -> None:
        cur = self.root
        for ch in word:
            if (ch not in cur.children):
                cur.children[ch] = TrieNode()
            cur = cur.children[ch]
        cur.endWord = True
        

    def search(self, word: str) -> bool:
        cur = self.root

        def dfs(root, index):
            cur = root
            if index == len(word):
                return (cur.endWord)
            if (word[index] == '.'):
                for node in cur.children.values():
                    if (dfs(node, index + 1)):
                        return True
            if (word[index] not in cur.children):
                return False
            cur = cur.children[word[index]]
            return (dfs(cur, index + 1))
        return(dfs(self.root, 0))

```
