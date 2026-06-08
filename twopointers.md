# DSA Two Pointers

When to use two pointers technique:

- Question is of Array or Linked List
- Data Sorted or can be sorted to make it easier to solve
- Merge / Remove duplicates / Rearrange
- Detect Cycle in Linked List
- Find pairs / triplets / subarrays

1. **Merge Two Sorted Arrays**: Given two sorted arrays, merge them into a single sorted array.

Leetocode: [Merge Two Sorted Arrays](https://leetcode.com/problems/merge-sorted-array/)
'''c++
class Solution {
public:
void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {

        vector<int> result;
        int i = 0;
        int j = 0;

        while(i < m && j < n) {
            if(nums1[i] <= nums2[j]) {
                result.push_back(nums1[i]);
                i++;
            }
            else {
                result.push_back(nums2[j]);
                j++;
            }
        }

        while(i < m) {
            result.push_back(nums1[i]);
            i++;
        }

        while(j < n) {
            result.push_back(nums2[j]);
            j++;
        }

        for(int k = 0; k < m + n; k++) {
            nums1[k] = result[k];
        }
    }

};
'''

2. **Remove Duplicates from Sorted Array**: Given a sorted array, remove the duplicates in-place such that each element appears only once and return the new length.

Leetocode: [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)
'''c++

class Solution {
public:
int removeDuplicates(vector<int>& nums) {
int i=0;
int k=1;
int j=1;
while(j<nums.size()){
if(nums[j] == nums[j-1]){
j++;
}
else{
nums[i+1]=nums[j];
i++;
k++;
j++;
}

      }
       return k;

}
};
''' 3. Square of a Sorted Array: Given an array of integers sorted in non-decreasing order, return an array of the squares of each number sorted in non-decreasing order.

Leetocode: [Squares of a Sorted Array](https://leetcode.com/problems/squares-of-a-sorted-array/)
'''c++
class Solution {
public:
vector<int> sortedSquares(vector<int>& nums) {
vector<int> neg, pos;

        for(int i = 0; i < nums.size(); i++) {
            if(nums[i] < 0)
                neg.push_back(nums[i] * nums[i]);
            else
                pos.push_back(nums[i] * nums[i]);
        }

        reverse(neg.begin(), neg.end());

        int i = 0, j = 0;
        vector<int> result;

        while(i < neg.size() && j < pos.size()) {
            if(neg[i] <= pos[j])
                result.push_back(neg[i++]);
            else
                result.push_back(pos[j++]);
        }

        while(i < neg.size())
            result.push_back(neg[i++]);

        while(j < pos.size())
            result.push_back(pos[j++]);

        return result;
    }

};
''' 4. **Two Sum II - Input Array Is Sorted**: Given an array of integers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number.

Leetocode: [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)
'''c++
class Solution {
public:
vector<int> twoSum(vector<int>& arr, int target) {
int left = 0;
int right = arr.size() - 1;

        while (left < right) {
            int sum = arr[left] + arr[right];

            if (sum == target) {
                return {left + 1, right + 1};
            }
            else if (sum < target) {
                left++;
            }
            else {
                right--;
            }
        }

        return {};
    }

};
