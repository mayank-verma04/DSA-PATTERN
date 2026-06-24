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

# 4 Find duplicate number in an array

**Problem statement**: Given an array nums containing n + 1 integers where each integer is in the range [1, n] inclusive. There is only one repeated number in nums, return this repeated number.

```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int slow =0;
        int fast=0;
      while(true){
        slow =nums[slow];
        fast=nums[fast];
        fast=nums[fast];
        if(slow == fast){
            slow = 0;
            while(slow!=fast){
                 slow =nums[slow];
                 fast=nums[fast];
            }
              return slow;
        }

      }
      return -1;
    }
};
```

# 5 Happy Number

**Problem statement**: Write an algorithm to determine if a number n is happy. A happy number is a number defined by the following process: Starting with any positive integer, replace the number by the sum of the squares of its digits, and repeat the process until the number equals 1 (where it will stay), or it loops endlessly in a cycle that does not include 1. Those numbers for which this process ends in 1 are happy numbers.

```cpp
class Solution {
public:
    // Find the square sum of the digits
    int sumOfSquareOfDigits(int n){
        int sum = 0;
        while(n>0){
            int digit = n % 10;
            n = n / 10;
            sum = sum + (digit*digit);
        }
        return sum;
    }
    bool isHappy(int n) {
        int slow = n;
        int fast = n;
        while (fast != 1){
            slow = sumOfSquareOfDigits(slow);
            fast = sumOfSquareOfDigits(fast);
            fast = sumOfSquareOfDigits(fast);
            if (slow == fast && slow != 1){
                return false;
            }
        }
        return true;
    }
};
```
