# When to use a sliding window

- Apply to strings or arrays.
- Question may ask for a contiguous subarray or substring.
- Question may ask for a maximum, minimum,longest,shortest,count,average.sum,exactly k or atleast k value of a subarray or substring.
- Sliding window is of two types:

- Fixed size sliding window
- Variable size sliding window

# 1 Find maximum sum of a subarray of size k

**Problem statement**: Given an array of integers and a number k, find the maximum sum of a subarray of size k.
**Geeks for Geeks solution**: [Maximum sum of a subarray of size k](https://www.geeksforgeeks.org/problems/max-sum-subarray-of-size-k5313/1)

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

**Problem statement**: Given an array of integers and a number k, find the minimum size of a contiguous subarray of which the sum is greater than or equal to k. If there isn't one, return 0 instead.
**Leetcode solution**: [Minimum size subarray sum](https://leetcode.com/problems/minimum-size-subarray-sum/description/)

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
