<https://leetcode.com/problems/contiguous-array/>

If we have a subarray with equal number of 0 and 1 starting at index `i` and ending at `j-1`, it means that in this subarray with `j-i` elements, there're a half `1`'s and a half `0`s that add up to `(j-i)/2`. In other words, the exclusive [prefix sum](https://en.wikipedia.org/wiki/Prefix_sum) at index `j` minus that at index `i` equals `(j-i)/2`, or `2*pre_sum[j]-j = 2*pre_sum[i]-i`.  We want to maximize the difference of `j` and `i` that satisfy the equation, so we can use a hash map to record the value of `2*pre_sum[i]-i` and its corresponding index `i`, and update the result with `j-i`.

```python
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        n = len(nums)
        if n < 2:
            return 0
        res = 0
        hashmap = {0: 0}
        pre_sum = nums[0]
        for j in range(1, n):
            term = 2*pre_sum - j
            if term in hashmap:
                res = max(res, j - hashmap[term])
            else:
                hashmap[term] = j
            pre_sum += nums[j]
        j = n
        if 2*pre_sum - j in hashmap:
            res = max(res, j - hashmap[2*pre_sum - j])
        return res
```

Alternatively, we can consider every `0` in the array as `-1` so that what we're looking for becomes a subarray with zero sum. Store the cumulative sum in a dict so that when the same value appears again, the length of the subarray can be calculated.

```python
class Solution:
    def findMaxLength(self, nums: List[int]) -> int:
        d = {0: -1}
        sum = 0
        res = 0
        for i, num in enumerate(nums):
            sum += (-1,1)[num]
            if sum not in d:
                d[sum] = i
            else:
                res = max(res, i - d[sum])
        return res
```

