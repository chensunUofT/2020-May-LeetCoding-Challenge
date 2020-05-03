<https://leetcode.com/problems/ransom-note/>

The easiest idea is to iterate over every character in the `ransomNote` string and remove the letter in the `magazine` string if it exists. The time complexity is `O(m+n)`.

```python
class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        m = list(magazine)
        for s in ransomNote:
            if s not in m:
                return False
            else:
                m.remove(s)
        return True
    
```

We can also use two Counters to store the occurrences of letters in the two strings and do an element-wise comparison to see if there're more occurrences in `magazine` than `ransomNote` for every letter in `ransomNote`. The time complexity is `O(m+n)`. 

```python
from collections import Counter

class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        r = Counter(ransomNote)
        m = Counter(magazine)
        for s in r.keys():
            if r[s] > m[s]:
                return False
        return True
    
```

(Learned from discussion) There is a smarter way of doing this: by substracting two Counter object using `-`, only positive counts are reserved, so we can figure out whether there's any letter than appears in `ransomNote` more than in`magazine`.

 ```python
from collections import Counter

class Solution:
    def canConstruct(self, ransomNote: str, magazine: str) -> bool:
        return not(Counter(ransomNote) - Counter(magazine))
    
 ```

