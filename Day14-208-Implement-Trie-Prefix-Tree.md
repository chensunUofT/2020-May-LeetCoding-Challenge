<https://leetcode.com/problems/implement-trie-prefix-tree/>

Use each `TrieNode` to represent a letter in the words, and use a `children` dict to store the children/sub-trees of the node that stands for the next letter.

```python
class Trie:

    class TrieNode:
        def __init__(self):
            self.is_leaf = False
            self.children = {}
    
    def __init__(self):
        """
        Initialize your data structure here.
        """
        self.root = self.TrieNode()
        

    def insert(self, word: str) -> None:
        """
        Inserts a word into the trie.
        """
        node = self.root
        for letter in word:
            if letter not in node.children:
                node.children[letter] = self.TrieNode()
            node = node.children[letter]
        node.is_leaf = True
        
    def search(self, word: str) -> bool:
        """
        Returns if the word is in the trie.
        """
        node = self.root
        for letter in word:
            if letter not in node.children:
                return False
            else:
                node = node.children[letter]
        return node.is_leaf
        

    def startsWith(self, prefix: str) -> bool:
        """
        Returns if there is any word in the trie that starts with the given prefix.
        """
        node = self.root
        for letter in prefix:
            if letter not in node.children:
                return False
            else:
                node = node.children[letter]
        return True
        

# Your Trie object will be instantiated and called as such:
# obj = Trie()
# obj.insert(word)
# param_2 = obj.search(word)
# param_3 = obj.startsWith(prefix)
```

