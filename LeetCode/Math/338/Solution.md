# 338. Counting Bits

Given a non negative integer number **num**. For every numbers **i** in the range **0 ≤ i ≤ num** calculate the number of 1's in their binary representation and return them as an array.

**Example 1:**

```
Input: 2
Output: [0,1,1]
```

**Example 2:**

```
Input: 5
Output: [0,1,1,2,1,2]
```

## Solution1

```C++
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> res;
        for (int x = 0; x <= num; x ++) {
            res.push_back(count(x));
        }
        return res;
    }
    
    int count(int x) {
        int n = 0;
        while (x) {
            if (x & 1) n ++;
            x >>= 1;
        }
        return n;
    }
};
```

​     