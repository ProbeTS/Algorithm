# 96. Unique Binary Search Trees

Given *n*, how many structurally unique **BST's** (binary search trees) that store values 1 ... *n*?

**Example:**

```
Input: 3
Output: 5
Explanation:
Given n = 3, there are a total of 5 unique BST's:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

## Solution

Catalan Number.

The recursion is as follows
$$
![](http://latex.codecogs.com/gif.latex?\C_n=C_{n-1} \frac {4*n-2} {n+1})
$$
The general term is as follows
$$
![](http://latex.codecogs.com/gif.latex?\\frac {C_{2n}^n} {n+1}) 
$$


```C++
class Solution {
public:
    long long numTrees(long long n) {
        if (n == 1)
            return 1;
        else 
            return numTrees(n - 1) * (4 * n - 2) / (n + 1);
    }
};
```

​     
