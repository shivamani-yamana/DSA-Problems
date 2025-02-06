# 50. Pow(x, n)
**Difficulty**: Medium  
**Algorithm**: Divide and Conquer

## Problem Description

Implement `pow(x, n)`, which calculates `x` raised to the power `n` (i.e., `x^n`).

### Example 1:
**Input**:  
`x = 2.00000, n = 10`  
**Output**:  
`1024.00000`

### Example 2:
**Input**:  
`x = 2.10000, n = 3`  
**Output**:  
`9.26100`

### Example 3:
**Input**:  
`x = 2.00000, n = -2`  
**Output**:  
`0.25000`

**Explanation**:  
`2^(-2) = 1/(2^2) = 1/4 = 0.25`

## Constraints:
- `-100.0 < x < 100.0`
- `-231 <= n <= 231-1`
- `n` is an integer.
- Either `x` is not zero or `n > 0`.
- `-10^4 <= x^n <= 10^4`

## Solution

```java
class Solution {
    public double myPow(double x, int n) {
        if(n == 0) return 1;
        else if (n == Integer.MIN_VALUE) return 1 / myPow(x, Integer.MAX_VALUE) * x;
        else if(n < 0) return 1 / myPow(x, -n);
        double half = myPow(x, n / 2);
        if(n % 2 == 0) {
            return half * half;
        } else {
            return x * half * half;
        }
    }
}
```

## Explanation

The approach uses the "divide and conquer" technique. If the exponent n is zero, we return 1 as anything raised to the power of 0 is 1. If n is negative, we compute the result for the positive exponent and then take its reciprocal. For other cases, we divide the exponent by 2 and recursively calculate x^(n/2). Finally, if n is odd, we multiply the result by x to account for the extra multiplication.

## Time Complexity:
The time complexity of the solution is O(log n) due to the recursive halving of the exponent n.

## Space Complexity:
The space complexity is O(log n) for the recursion stack.
