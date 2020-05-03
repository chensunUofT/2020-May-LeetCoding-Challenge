<https://leetcode.com/problems/jewels-and-stones/>

There're quite a few ways to solve this problem:

- We can use a `Counter` to extract the occurrences of each item in `S`, and sum up the count for those in `J`

  ```python
  from collections import Counter
  
  class Solution:
      def numJewelsInStones(self, J: str, S: str) -> int:
          return sum(Counter(S)[item] for item in J)
  ```

- We can sum up the Boolean value whether or not each item in `S` is in `J` as well:

  ```python
  class Solution:
      def numJewelsInStones(self, J: str, S: str) -> int:
      	return sum(stone in J for stone in S)
  ```

- (Learned from [Discussion](https://leetcode.com/problems/jewels-and-stones/discuss/?currentPage=1&orderBy=most_votes&query=)) Use the `list.count(x)` method. This can be combined with the [`map`](https://docs.python.org/3/library/functions.html#map) built-in function:

  ```python
  class Solution:
      def numJewelsInStones(self, J: str, S: str) -> int:
          return sum(map(S.count, J))
  ```
  
  ```python
  class Solution:
      def numJewelsInStones(self, J: str, S: str) -> int:
          return sum(map(J.count, S))
  ```
  
  