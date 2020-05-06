<https://leetcode.com/problems/majority-element/>

We can certainly use a Dictionary or Counter to figure out the occurrences of all the elements and find the majority one, which takes `O(n)` time and `O(n)` space, but there're some other solutions.

If number `k` is the majority in the list, then the median of the (sorted) array has to be `k`. So we can sort the array and return the median with `O(nlogn)` time and `O(1)` space.

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        return sorted(nums)[len(nums)//2]
```

A smarter way to solve this problem is [Boyer–Moore majority vote algorithm](https://en.wikipedia.org/wiki/Boyer–Moore_majority_vote_algorithm)

![](https://upload.wikimedia.org/wikipedia/commons/thumb/c/c7/Boyer-Moore_MJRTY.svg/1920px-Boyer-Moore_MJRTY.svg.png)

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        count = 0
        for num in nums:
            if count == 0:
                maj = num
                count = 1
            elif num == maj:
                count += 1
            else:
                count -= 1
        return maj
```

