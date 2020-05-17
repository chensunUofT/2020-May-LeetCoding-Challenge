<https://leetcode.com/problems/find-all-anagrams-in-a-string/>

Checking if two strings are anagrams of each other is equivalent of comparing the occurrences of each character in the two strings. The `Counter` class would be really handy for the task.  
To find the starting index of all the substrings that satisfy the requirement, the idea of sliding window can be used: in each iteration, remove the first letter in the substring from the counter and add the next letter into it. As long as the two counters are equal, add the starting index to the result.

```python
from collections import Counter

class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        k = len(p)
        target_cnt = Counter(p)
        res = []
        cnt = Counter(s[:k])
        if cnt == target_cnt:
            res.append(0)
        for i in range(1, len(s)-k+1):
            cnt[s[i-1]] -= 1
            cnt[s[i+k-1]] += 1
            if +cnt == target_cnt:
                res.append(i)
        return res
```

A trick here is to use `+cnt`, which only includes keys with positive values, instead of `cnt` when comparing two counters.

We can also use an array (a list, to be accurate) of length 26 to represent the frequency of letters in the string. `ord(letter) - ord('a')` creates a mapping from `'a', 'b', ..., z'` to `0, 1, ..., 25`.

```python
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        target = [0] * 26
        for letter in p:
            target[ord(letter)-ord('a')] += 1
        cnt = [0] * 26
        k = len(p)
        for letter in s[:k]:
            cnt[ord(letter)-ord('a')] += 1
        if cnt == target:
            res = [0]
        else:
            res = []
        for i in range(1, len(s)-k+1):
            cnt[ord(s[i-1])-ord('a')] -= 1
            cnt[ord(s[i+k-1])-ord('a')] += 1
            if cnt == target:
                res.append(i)
        return res
```

