# DSA - Slow and Fast Pointers

When to use the slow and fast pointer technique?

- Finding loop, repetition, or cycle in any data structure (like linked list, array, etc.)

- Finding the middle element of a linked list or array.

# 1 Detecting a cycle in a linked list

**Problem statement**: Given a linked list, determine if it has a cycle in it.

```cpp
class Solution {
public:
    bool hasCycle(ListNode *head) {
      ListNode *slow=head;
      ListNode *fast=head;

      while(fast != NULL && fast->next != NULL){
      slow = slow ->next;
      fast= fast->next->next;
       if(slow == fast){
        return true;
      }
      }
      return false;
    }
};
```
