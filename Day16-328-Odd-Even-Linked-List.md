<https://leetcode.com/problems/odd-even-linked-list/>

Firstly use two pointers to generate an "odd list" and an "even list" by connecting all the "odd nodes" and "even nodes" together respectively, then append the "even" list to the end of the "odd" list.

```python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next

class Solution:
    def oddEvenList(self, head: ListNode) -> ListNode:
        if not head or not (head.next) or not (head.next.next):
            return head
        odd_head, even_head = head, head.next
        odd, even = odd_head, even_head
        while (odd.next and even.next):
            odd.next = even.next
            odd = odd.next
            even.next = odd.next
            even = even.next
        odd.next = even_head
        return odd_head
```



