# 74. Search a 2D Matrix

Write an efficient algorithm that searches for a value in an *m* x *n* matrix. This matrix has the following properties:

- Integers in each row are sorted from left to right.
- The first integer of each row is greater than the last integer of the previous row.

**Example 1:**

```
Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 3
Output: true
```

**Example 2:**

```
Input:
matrix = [
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
target = 13
Output: false
```

## Solution

We can solve the problem by the double pointer algorithm.

We select the point in the upper right corner which is guaranteed that it is larger than all the left points in the same row as it and smaller than all the lower points in the same column as it. Then we can find the target position by comparing the numbers. 

```C++
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        if (matrix.empty()) return false;
        int row = matrix.size(), col = matrix[0].size();
        int i = 0, j = col - 1;
        while (i < row && j >= 0) {
            if (matrix[i][j] < target)
                i ++;
            else if (matrix[i][j] > target)
                j --;
            else 
                return true;
        }
        return false;
    }
};
```

​     