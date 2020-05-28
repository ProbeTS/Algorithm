# 231. Power of Two

Given an integer, write a function to determine if it is a power of two.

**Example 1:**

```
Input: 1
Output: true 
Explanation: 20 = 1
```

**Example 2:**

```
Input: 16
Output: true
Explanation: 24 = 16
```

**Example 3:**

```
Input: 218
Output: false
```

## Solution

Suppose a power of two is n. The most significant bit of the binary number n is 1 and other bits are 0. In contrast, all the bits of n-1 is 1 so the result of the and operation is 0 if n is a power of two.

We can give an example.

16 = 10000b

16-1=15=1111b

16 & 15 = 10000b & 1111b = 0  

```C++
class Solution {
public:
    bool isPowerOfTwo(long long n) {
        if (n == 0) return false;
        return !(n & (n-1));
    }
};
```

​     