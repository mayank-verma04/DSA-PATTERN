# When to use a sliding window

- Apply to strings or arrays.
- Question may ask for a contiguous subarray or substring.
- Question may ask for a maximum, minimum,longest,shortest,count,average.sum,exactly k or atleast k value of a subarray or substring.
- Sliding window is of two types:

- Fixed size sliding window
- Variable size sliding window

# 1 Find maximum sum of a subarray of size k

```cpp
class Solution {
  public:
    int maxSubarraySum(vector<int>& arr, int k) {
        // code here
        int low = 0;
        int high = k-1;
        int res=INT_MIN;
        int sum=0;

    //Calculate first sum
    for(int i=low;i<=high;i++){
        sum=sum+arr[i];
    }
    // Iterate through by calculating complete sum
    while(high<arr.size()){
        res = max(res,sum);
        low++;
        high++;
        if(high == arr.size()){
            break;
        }
        sum = sum-arr[low-1];
        sum = sum + arr[high];
    }
    return res;
    }
};
```

# 2 Minimum size subarray sum

```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& arr) {
        int low=0;
        int high=0;
        int res=INT_MAX;
        int sum =0;
        for(int high=0;high<arr.size();high++){
            sum=sum + arr[high];
            while(sum>=target){
                int length = high - low + 1;
                res=min(length,res);
                sum-=arr[low];
                low++;
            }
        }
        return (res==INT_MAX)?0:res;
    }

};
```

# 3 Longest Substring with K Uniques

```cpp
class Solution {
public:
    int longestKSubstr(string &s, int k) {
        int low = 0;
        unordered_map<char, int> freq;
        int res = -1;

        for (int high = 0; high < s.size(); high++) {
            freq[s[high]]++;

            while (freq.size() > k) {
                freq[s[low]]--;

                if (freq[s[low]] == 0) {
                    freq.erase(s[low]);
                }

                low++;
            }

            if (freq.size() == k) {
                int length = high - low + 1;
                res = max(res, length);
            }
        }

        return res;
    }
};
```

# 4 Fruit Into Baskets

```cpp
class Solution {
public:
    int totalFruit(vector<int>& fruits) {
        unordered_map<int, int> freq;
        int left = 0;
        int maxLen = 0;
        for (int right = 0; right < fruits.size(); right++) {
            freq[fruits[right]]++;
            // Shrink window if distinct characters exceed 2
            while (freq.size() > 2) {
                freq[fruits[left]]--;
                if (freq[fruits[left]] == 0) {
                    freq.erase(fruits[left]);
                }
                left++;
            }
            // Update answer when exactly 2 distinct characters exist
            maxLen = max(maxLen, right - left + 1);
        }
        return maxLen;
    }
};
```

# 5 Longest Substring Without Repeating Characters

```cpp
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> freq;
        int left = 0;
        int maxLen = 0;
        for (int right = 0; right < s.size(); right++) {
            freq[s[right]]++;
            int k = right - left + 1;
            while (freq.size() < k) {
                freq[s[left]]--;
                if (freq[s[left]] == 0) {
                    freq.erase(s[left]);
                }
                left++;
                k = right - left + 1;
            }
            maxLen = max(maxLen, right - left + 1);
        }
        return maxLen;
    }
};
```

# 6 Longest Repeating Character Replacement

```cpp
class Solution {
public:

    int findMax(vector<int>& arr) {
        int maxi = 0;
        for (int ch : arr) {
            maxi = max(maxi, ch);
        }
        return maxi;
    }

    int characterReplacement(string s, int k) {
        vector<int> arr(256, 0);

        int low = 0, res = 0;

        for (int high = 0; high < s.size(); high++) {
            arr[s[high]]++;

            int maxcount = findMax(arr);

            while ((high - low + 1) - maxcount > k) {
                arr[s[low]]--;
                low++;
                maxcount = findMax(arr);
            }

            res = max(res, high - low + 1);
        }

        return res;
    }
};
```
