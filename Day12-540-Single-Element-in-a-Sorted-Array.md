<https://leetcode.com/problems/single-element-in-a-sorted-array/>

Note that the single element would only appear after a number of pairs, i.e. the index of the single element would always be a even number in the form of `2*k`. Therefore, use a binary search to find the value of `k` so that `nums[2*k]` is the single element:

- If `nums[2*mid] == nums[2*mid + 1]`, it implies that all the elements from `nums[low]` to `nums[2*mid + 1]` are in pairs, so the index of the single element must be greater or equal than `nums[2*(mid+1)]`;
- Otherwise, the elements from `nums[low]` to `nums[2*mid - 1]` are not in pairs, so the search range of `k` should be set to `[low, mid]`.

When `low == high`, the range of `k` is limited in one number, and the value of `nums[2*k]` is the single element that we want to find.

```python
class Solution:
    def singleNonDuplicate(self, nums: List[int]) -> int:
        low, high = 0, len(nums) // 2
        while low < high:
            mid = (low + high) // 2
            if nums[2*mid] == nums[2*mid + 1]:
                low = mid + 1
            else:
                high = mid
        return nums[2*low]
```

