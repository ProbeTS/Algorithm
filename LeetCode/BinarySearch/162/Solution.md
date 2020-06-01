# 162. Find Peak Element

A peak element is an element that is greater than its neighbors.

Given an input array `nums`, where `nums[i] ≠ nums[i+1]`, find a peak element and return its index.

The array may contain multiple peaks, in that case return the index to any one of the peaks is fine.

You may imagine that `nums[-1] = nums[n] = -∞`.

**Example 1:**

```
Input: nums = [1,2,3,1]
Output: 2
Explanation: 3 is a peak element and your function should return the index number 2.
```

**Example 2:**

```
Input: nums = [1,2,1,3,5,6,4]
Output: 1 or 5 
Explanation: Your function can return either index number 1 where the peak element is 2, 
             or index number 5 where the peak element is 6.
```

## Solution1

We can solve the problem by linear scan. We just compare nums[i] with nums[i+1] and return i when nums[i] > nums[i+1]. We needn't compare nums[i] with nums[i-1] because we can't reach i if nums[i-1] > nums[i].

```C++
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        for (int i = 0; i < nums.size() - 1; i ++) {
            if (nums[i] > nums[i+1]) {
                return i; 
            }
        }
        return nums.size() - 1;
    }
};
```

## Solution2

We can apply binary search and recursion to this problem.

```c++
class Solution {
public:
    int findPeakElement(vector<int>& nums) {
        return search(nums, 0, nums.size()-1);
    }
    
    int search(vector<int>& nums, int l, int r) {
        if (l == r) 
            return l;
        int mid = l + r >> 1;
        if (nums[mid] > nums[mid + 1])
            return search(nums, l, mid);
        return search(nums, mid + 1, r);
    }
};
```

