# 1. Two Sum

Given an array of integers, return **indices** of the two numbers such that they add up to a specific target.

You may assume that each input would have **exactly** one solution, and you may not use the *same* element twice.

## Solution
'''
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> umap;
        for (int i = 0; i < nums.size(); i ++) {
            if (umap.count(target - nums[i])) 
                return {umap[target - nums[i]], i};
            umap[nums[i]] = i;
        }
        return {};
    }
};
'''
