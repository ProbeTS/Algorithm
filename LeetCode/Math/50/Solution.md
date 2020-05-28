# 50. Pow(x, n)

Implement [pow(*x*, *n*)](http://www.cplusplus.com/reference/valarray/pow/), which calculates *x* raised to the power *n* (x^n). 

**Example 1:**

```
Input: 2.00000, 10
Output: 1024.00000
```

**Example 2:**

```
Input: 2.10000, 3
Output: 9.26100
```

**Example 3:**

```
Input: 2.00000, -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25
```

## Solution

We apply the **binary exponentiation** algorithm to solve the problem. 

```C++
class Solution {
public:
    double myPow(double x, long long n) {
        if (n < 0) 
            return 1 / qmi(x, -n);
        return qmi(x, n);
    }
    
    double qmi(double x, long long n) {
        double res = 1;
        while (n) {
            if (n & 1) res *= x;
            x = x * x;
            n = n >> 1;
        }
        return res;
    }
};
```

​     