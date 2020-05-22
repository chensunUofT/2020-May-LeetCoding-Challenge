<https://leetcode.com/problems/sort-characters-by-frequency/>

We can use an idea similar with bucket sort: put all the letters in an array `bucket` so that `bucket[i]` contains all the letters that appear `i` times in the raw string. Then traverse the array reversely and add every letter with corresponding number of copies to the result.

```python
class Solution:
    def frequencySort(self, s: str) -> str:
        cnt = {}
        for letter in s:
            if letter in cnt:
                cnt[letter] += 1
            else:
                cnt[letter] = 1
        bucket = [[] for _ in range(len(s) + 1)]
        for letter, freq in cnt.items():
            bucket[freq].append(letter)
        res = ''
        for i in range(len(s), 0, -1):
            for letter in bucket[i]:
                res += letter * i
        return res
```

Alternatively, we can use `Counter` to get the frequency of each letter, and use the `most_common()` method to get the keys and values in the value with descending order.

```python
from collections import Counter

class Solution:
    def frequencySort(self, s: str) -> str:
        cnt = Counter(s)
        res = [char * num for (char, num) in cnt.most_common()]
        return ''.join(res)
```

