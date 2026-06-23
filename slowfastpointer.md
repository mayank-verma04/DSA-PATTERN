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

# 2 Retuen the starting node of the cycle in a linked list

**Problem statement**: Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode *slow = head;
        ListNode *fast = head;

        while (fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;

            if (slow == fast) {
                slow = head;

                while (slow != fast) {
                    slow = slow->next;
                    fast = fast->next;
                }

                return slow;  // start of cycle
            }
        }

        return NULL; // no cycle
    }
};
```

# 3 Finding the middle node of a linked list

**Problem statement**: Given a non-empty, singly linked list with head node head, return a middle node of linked list. If there are two middle nodes, return the second middle node.

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode *slow = head;
        ListNode *fast = head;
        while(fast!=NULL && fast->next!=NULL){
            slow = slow->next;
            fast = fast->next->next;
        }
        return slow;
    }
};
```
