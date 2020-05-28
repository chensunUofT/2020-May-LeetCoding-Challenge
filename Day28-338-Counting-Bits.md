<https://leetcode.com/problems/counting-bits/>

The first solution comes from the hint that the numbers can be divided in ranges like [1], [2-3], [4-7], [8-15] etc. so that each range is from `2**l` to `2**(l+1) - 1` where `l` is the flooring rounded of base 2 log of `num`, and we can observe these ranges:

| num  | binary | bits | log2num |
| :--: | :----: | :--: | :-----: |
|  0   |   0    |  0   |         |
|      |        |      |    0    |
|  1   |   1    |  1   |         |
|      |        |      |    1    |
|  2   |   10   |  1   |         |
|  3   |   11   |  2   |         |
|      |        |      |    2    |
|  4   |  100   |  1   |         |
|  5   |  101   |  2   |         |
|  6   |  110   |  2   |         |
|  7   |  111   |  3   |         |
|      |        |      |    3    |
|  8   |  1000  |  1   |         |
|  9   |  1001  |  2   |         |
|  10  |  1010  |  2   |         |
|  11  |  1011  |  3   |         |
|  12  |  1100  |  2   |         |
|  13  |  1101  |  3   |         |
|  14  |  1110  |  3   |         |
|  15  |  1111  |  4   |         |

We can find that the `bits` values of the new range (for example `1,2,2,3,2,3,3,4`) consist of an original duplicate of the previous range (`1,2,2,3`) and another duplicate where each value increases by 1 (`2,3,3,4`). Therefore, we can iteratively generate the bits array using the previous one for `log2num` times and extend them to the result. For the remaining numbers greater than `2**log2num - 1`, use a slice of the next range.

```python
class Solution:
    def countBits(self, num: int) -> List[int]:
        if num == 0:
            return [0]
        if num == 1:
            return [0,1]
        log2num = 0
        k = num
        while k > 1:
            log2num += 1
            k = k // 2
        res = [0]
        prev = [1]
        for i in range(log2num):
            res.extend(prev)
            prev.extend([element + 1 for element in prev])
        res.extend(prev[:num - 2 ** log2num + 1])
        return res
```

To look at it another way, each time the array doubles it size, it is extended by a duplicate where each element is incremented by 1.

```python
class Solution:
    def countBits(self, num: int) -> List[int]:
        res = [0]
        while len(res) <= num:
            res.extend([i+1 for i in res])
        return res[:num+1]
```

Alternatively, if we look at the binary representation of each number `i`(for example `101` for `5`), the last bit is the "odd-even" bit which equals to `i % 2`, and the other bits are identical to the bits of `i // 2` or `i >> 1`. Therefore, we can use the result for `i >> 1` to calculate the bits for `i`.

```python
class Solution:
    def countBits(self, num: int) -> List[int]:
        res = [0]
        for i in range(1, num + 1):
            res.append(res[i>>1] + (i % 2))
        return res
```

Yet another algorithm is that we can set the right-most `1` to `0` in number `i` by calculating `i & (i-1)` so that the number of bits for number `i` can be calculated with previous results.

```python
class Solution:
    def countBits(self, num: int) -> List[int]:
        res = [0]
        for i in range(1, num + 1):
            res.append(res[i&(i-1)] + 1)
        return res
```

