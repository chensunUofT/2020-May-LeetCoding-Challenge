<https://leetcode.com/problems/remove-k-digits/>

The *Greedy* idea here is that, we can always get the smallest value after deletion if we remove the **first digit which is greater than the digit after it**, e.g. in `1432219`, `1` is not greater than `4`, but `4` is greater `1`, so by deleting `4` we get the smallest result `132219`. If every digit is not greater than the next one, just remove the last digit.

 ```python
class Solution:
    def removeKdigits(self, num: str, k: int) -> str:
        if not k:
            return num
        if k >= len(num):
            return "0"
        for i in range(len(num)-1):
            if int(num[i]) > int(num[i+1]):
                num = num[:i] + num[i+1:]
                return self.removeKdigits(num.lstrip('0') or '0', k-1)
        return self.removeKdigits(num[:-1], k-1)
 ```

The time complexity of the algorithm above is `O(kn)`. Using a stack to store the digits and popping those digits greater than the new element can optimize it to `O(n)` time:

```python
class Solution:
    def removeKdigits(self, num: str, k: int) -> str:
        stack = []
        for s in num:
            while stack and k and s < stack[-1]:
                stack.pop()
                k -= 1
            stack.append(s)
        return ''.join(stack[:-k or None]).lstrip('0') or '0'
```

A Pythonic trick here is the `stack[:-k or None]` as [explained here](https://stackoverflow.com/questions/15627312/what-value-do-i-use-in-a-slicing-range-to-include-the-last-value-in-a-numpy-arra/15627413#15627413). If `k` is greater than `0`, `stack[:-k]` will definitely give you the list without the last `k` elements, which is want we want; However, `stack[:-0]`, which is equivalent to `stack[:0]`, returns an empty list instead of the whole list itself as we expect.  
To fix that, use `-k or None` as the ending index of the list, so that when `k` equals `0`, `0 or None` gives you a `None` and `stack[:None]` is just `stack` as discussed [here](https://stackoverflow.com/questions/30622809/python-list-slicing-with-none-as-argument).

