<https://leetcode.com/problems/online-stock-span/>

Use a stack to store the `price` value and the corresponding `res` (maximum numbers of consecutive days with value less than or equal to the value of that day).  Every time when a new `price` comes, keep popping the top of the stack and accumulating the `res` value until the stack gets empty or a greater value is met, then push the `price` and `res` into the stack.

```python
class StockSpanner:

    def __init__(self):
        self.stack = []

    def next(self, price: int) -> int:
        res = 1
        while self.stack and self.stack[-1][0] <= price:
            res += self.stack.pop()[1]
        self.stack.append((price, res))
        return res


# Your StockSpanner object will be instantiated and called as such:
# obj = StockSpanner()
# param_1 = obj.next(price)
```

