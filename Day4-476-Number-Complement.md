<https://leetcode.com/problems/number-complement/>  
<https://leetcode.com/problems/complement-of-base-10-integer/>

We can solve this problem with a pure numerical approach: find the last binary bit by `num % 2`, and add the corresponding "complemented" value to the result. The left and right shifts are faster alternatively to multiplying and dividing by 2.

```python
class Solution:
    def findComplement(self, num: int) -> int:
        res = 0
        bit_value = 1
        while num:
            res += (1 - num % 2) * bit_value
            num >>= 1
            bit_value <<= 1
        return res
```

This problem can also be solved by string operations: converting the number to the binary string, replacing each character in it, and converting back to decimal integer.

```python
class Solution:
    def findComplement(self, num: int) -> int:
        
        def convert_string(s):
            return ''.join([str(int(char=='0')) for char in s])
        
        binary = format(num, 'b')
        binary_converted = convert_string(binary)
        return int(binary_converted, 2)
```

There're some amazing solutions from discussion:

- Firstly finding the smallest number with the binary format as `100...` as `mask`, then doing a bit-wise XOR operation with `mask-1` (which is `111...` in binary with the same length as the input).

  ```python
  class Solution(object):
      def findComplement(self, num):
          i = 1
          while i <= num:
              i = i << 1
          return (i - 1) ^ num
  ```

- Flipping each bit with bit operation:

  ```python
  class Solution(object):
      def findComplement(self, num):
          i = 1
          while num >= i:
              num ^= i
              i <<= 1
          return num
  ```

  