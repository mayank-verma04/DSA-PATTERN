# DSA - Slow and Fast Pointers

When to use the slow and fast pointer technique?

- Finding loop, repetition, or cycle in any data structure (like linked list, array, etc.)

- Finding the middle element of a linked list or array.

# 1 Detecting a cycle in a linked list

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

# 2 Return the starting node of the cycle in a linked list

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
