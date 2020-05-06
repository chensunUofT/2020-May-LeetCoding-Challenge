<https://leetcode.com/problems/first-unique-character-in-a-string/>

Use a counter to find out the occurrences of each character in the string, then return the index of the first letter with count 1.

```python
from collections import Counter

class Solution:
    def firstUniqChar(self, s: str) -> int:
        cnt = Counter(s)
        for i, char in enumerate(s):
            if cnt[char] == 1:
                return i
        return -1
```

