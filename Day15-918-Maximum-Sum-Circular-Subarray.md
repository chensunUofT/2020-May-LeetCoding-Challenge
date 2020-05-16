<https://leetcode.com/problems/maximum-sum-circular-subarray/>

The maximum sum in the circular array comes from either:

- A non-circular subarray, which can be found using the same algorithm ([Kadane's Algorithm](https://en.wikipedia.org/wiki/Maximum_subarray_problem#Kadane's_algorithm)) as in [53. Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
- A circular subarray which consists of a "head part" and a "tail part" of the original array. The key idea here is that, the maximum sum of circular subarrays, is the exactly **the sum of the whole array minus the minimum sum of non-circular subarrays**. The minimum subarray could be found using similar approach.

<img src="https://assets.leetcode.com/users/motorix/image_1538888300.png" alt="image" style="zoom: 80%;" />

A corner case here is that, if every element in the array is negative, then the minimum subarray would be just the whole array and the difference between the two arrays would be `0` (the maximum subarray being empty) which does not satisfy the requirement that the maximum subarray could not be empty. To tackle that, check if the maximum element of the array is negative: if yes, then the every element is negative, so the maximum subarray would be the maximum single element in it.

```python
class Solution:
    def maxSubarraySumCircular(self, A: List[int]) -> int:
        if max(A) < 0:
            return max(A)
        cur_max_sum, max_sum, cur_min_sum, min_sum = [A[0]] * 4
        for num in A[1:]:
            cur_max_sum = max(num, cur_max_sum + num)
            max_sum = max(max_sum, cur_max_sum)
            cur_min_sum = min(num, cur_min_sum + num)
            min_sum = min(min_sum, cur_min_sum)
        return max(max_sum, sum(A)- min_sum)
```

Another solution is similar with the idea [here](https://leetcode.com/problems/maximum-subarray/discuss/20396/Easy-Python-Way): iteratively adding the previous element if it is greater than 0 so that it may contribute to the maximum value.

```python
class Solution:
    def maxSubarraySumCircular(self, A: List[int]) -> int:
        if max(A) < 0:
            return max(A)
        max_sum, min_sum = A[:], A[:]
        for i in range(1,len(A)):
            max_sum[i] += max(0, max_sum[i-1])
            min_sum[i] += min(0, min_sum[i-1])
        return max(max(max_sum), sum(A)-min(min_sum))
```

