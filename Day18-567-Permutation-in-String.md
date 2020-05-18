<https://leetcode.com/problems/permutation-in-string/>

Almost the same as the [438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/): [my solution](https://gist.github.com/chensunUofT/33f2938685177e7fc560fe32bd078351).

```python
class Solution:
    def checkInclusion(self, s1: str, s2: str) -> bool:
        target = [0] * 26
        for letter in s1:
            target[ord(letter)-ord('a')] += 1
        cnt = [0] * 26
        k = len(s1)
        for letter in s2[:k]:
            cnt[ord(letter)-ord('a')] += 1
        if cnt == target:
            return True
        for i in range(1, len(s2)-k+1):
            cnt[ord(s2[i-1])-ord('a')] -= 1
            cnt[ord(s2[i+k-1])-ord('a')] += 1
            if cnt == target:
                return True
        return False
```

