# DSA: Two Pointers Technique

## When to Use Two Pointers?

The Two Pointers technique is commonly used when:

- The problem involves Arrays or Linked Lists.
- The data is already sorted or can be sorted.
- You need to merge multiple sequences.
- You need to remove duplicates.
- You need to rearrange elements in-place.
- You need to find pairs, triplets, or subarrays.
- You need to detect cycles in a Linked List.

---

# 1. Merge Two Sorted Arrays

```cpp
class Solution {
public:
    void merge(vector<int>& nums1, int m,
               vector<int>& nums2, int n) {

        vector<int> result;
        int i = 0;
        int j = 0;

        while (i < m && j < n) {
            if (nums1[i] <= nums2[j]) {
                result.push_back(nums1[i]);
                i++;
            } else {
                result.push_back(nums2[j]);
                j++;
            }
        }

        while (i < m) {
            result.push_back(nums1[i]);
            i++;
        }

        while (j < n) {
            result.push_back(nums2[j]);
            j++;
        }

        for (int k = 0; k < m + n; k++) {
            nums1[k] = result[k];
        }
    }
};
```

---

# 2. Remove Duplicates from Sorted Array

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {

        if (nums.empty())
            return 0;

        int i = 0;
        int k = 1;
        int j = 1;

        while (j < nums.size()) {

            if (nums[j] == nums[j - 1]) {
                j++;
            } else {
                nums[i + 1] = nums[j];
                i++;
                k++;
                j++;
            }
        }

        return k;
    }
};
```

---

# 3. Squares of a Sorted Array

```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {

        vector<int> neg;
        vector<int> pos;

        for (int i = 0; i < nums.size(); i++) {

            if (nums[i] < 0) {
                neg.push_back(nums[i] * nums[i]);
            } else {
                pos.push_back(nums[i] * nums[i]);
            }
        }

        reverse(neg.begin(), neg.end());

        int i = 0;
        int j = 0;

        vector<int> result;

        while (i < neg.size() && j < pos.size()) {

            if (neg[i] <= pos[j]) {
                result.push_back(neg[i]);
                i++;
            } else {
                result.push_back(pos[j]);
                j++;
            }
        }

        while (i < neg.size()) {
            result.push_back(neg[i]);
            i++;
        }

        while (j < pos.size()) {
            result.push_back(pos[j]);
            j++;
        }

        return result;
    }
};
```

---

# 4. Two Sum II - Input Array Is Sorted

```cpp
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
```

# 5. Three Sum - Find all unique triplets in the array which gives the sum of zero.

```cpp
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> result;
        sort(nums.begin(), nums.end());

        for (int i = 0; i < nums.size() - 2; i++) {
            int left = i + 1;
            int right = nums.size() - 1;

            if (i > 0 && nums[i] == nums[i - 1]) {
                continue;
            }
            while (left < right) {
                if (nums[left] + nums[right] == -1 * nums[i]) {
                    result.push_back({nums[i], nums[left], nums[right]});
                    left++;
                    right--;
                    while (left < nums.size() - 1 &&
                           nums[left] == nums[left - 1]) {
                        left++;
                    }
                    while (right > 0 && nums[right] == nums[right + 1]) {
                        right--;
                    }
                } else if (nums[left] + nums[right] < -1 * nums[i]) {
                    left++;
                } else {
                    right--;
                }
            }
        }
        return result;
    }
};
```

# 6 Close to Target Sum - Find the sum of three integers in the array that is closest to a given target.

```cpp
class Solution {
public:
    int threeSumClosest(vector<int>& nums, int target) {

        sort(nums.begin(), nums.end());

        int result = nums[0] + nums[1] + nums[2];
        int max_diff = INT_MAX;

        for(int i = 0; i < nums.size() - 2; i++) {

            int left = i + 1;
            int right = nums.size() - 1;

            while(left < right) {

                int sum = nums[i] + nums[left] + nums[right];

                if(abs(target - sum) < max_diff) {
                    max_diff = abs(target - sum);
                    result = sum;
                }

                if(target == sum)
                    return sum;

                if(sum < target)
                    left++;
                else
                    right--;
            }
        }

        return result;
    }
};
```

# 7 Triplets less than Target - Find the number of triplets in the array such that the sum of the triplet is less than a given target.

```cpp
class Solution {
  public:
    int countTriplets(int sum, vector<int>& arr) {
        sort(arr.begin(), arr.end());

        int ans = 0;
        int n = arr.size();

        for(int i = 0; i < n - 2; i++) {
            int left = i + 1;
            int right = n - 1;
            while(left < right) {
                int curr = arr[i] + arr[left] + arr[right];
                if(curr < sum) {
                    ans += (right - left);
                    left++;
                } else {
                    right--;
                }
            }
        }

        return ans;
    }
};
```

# 8 Sort Colors - Given an array with n objects colored red, white, or blue, sort them in-place so that objects of the same color are adjacent, with the colors in the order red, white, and blue.

```cpp
class Solution {
public:
    void sortColors(vector<int>& nums) {
      int low =0;
      int mid=0;
      int high = nums.size()-1;
      while(mid<=high){
        if(nums[mid]==0){
            swap(nums[low],nums[mid]);
            low++;
            mid++;
        }
        else if(nums[mid]==2){
            swap(nums[high],nums[mid]);
            high--;
        }
        else{
         mid++;
        }}
      }
};
```
