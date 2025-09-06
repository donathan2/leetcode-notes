# LeetCode 208: Implement Trie (Prefix Tree) (Medium)
### Problem Description:

A trie (pronounced as "try") or prefix tree is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.

Implement the Trie class:

Trie() Initializes the trie object.

void insert(String word) Inserts the string word into the trie.

boolean search(String word) Returns true if the string word is in the trie (i.e., was inserted before), and false otherwise.

boolean startsWith(String prefix) Returns true if there is a previously inserted string word that has the prefix prefix, and false otherwise.


### Approach:

**Time complexity: O(n)**

**Space complexity: O(t) (nodes in trie)**

Understanding tries really is all there is to this problem. A trie node represents a lowercase character in the alphabet, but doesn't need that character as an explicit field as 
we hold these nodes as values to the keys that represent their characters. We hold this dictionary as the children for each node.

Originally I didn't think we needed an end word field because logically, if we come across a word and there's no children, then that has to be the end of the word. But there's also cases
where a word was already inputted in the trie, but is hidden within a longer word with the same prefix. For example, if we input banana and then ban, ban is a valid word but does have children,
so we would need some kind of field to indicate the end of a word for each node. It's really simple to implement as we simply set the end word field for the last node we've 
traversed in the insert method to true. It doesn't need to be touched anywhere else.

For the rest of the functions, it's just iterating through the word and checking their dictionary key status along the current node we're traversing. Fairly simple!


``` python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.wordEnd = False

class Trie:

    def __init__(self):
        self.root = TrieNode()
        
    def insert(self, word: str) -> None:
        cur = self.root

        for ch in word:
            if (ch not in cur.children):
                cur.children[ch] = TrieNode()
            cur = cur.children[ch]
        cur.wordEnd = True
                
    def search(self, word: str) -> bool:
        cur = self.root
        for ch in word:
            if (ch not in cur.children):
                return False
            cur = cur.children[ch]
        return (cur.wordEnd)
        
            
    def startsWith(self, prefix: str) -> bool:
        cur = self.root
        for ch in prefix:
            if (ch not in cur.children):
                return False
            cur = cur.children[ch]
        return True

```
