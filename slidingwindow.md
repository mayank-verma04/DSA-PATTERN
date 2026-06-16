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
