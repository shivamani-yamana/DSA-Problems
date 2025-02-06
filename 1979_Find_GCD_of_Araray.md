# 1979. Find Greatest Common Divisor of Array

## Problem Statement
Given an integer array `nums`, return the greatest common divisor of the smallest number and largest number in `nums`.

The greatest common divisor of two numbers is the largest positive integer that evenly divides both numbers.

### Example 1:
**Input:** `nums = [2,5,6,9,10]`  
**Output:** `2`  
**Explanation:**  
The smallest number in `nums` is `2`.
The largest number in `nums` is `10`.
The greatest common divisor of `2` and `10` is `2`.

### Example 2:
**Input:** `nums = [7,5,6,8,3]`  
**Output:** `1`  
**Explanation:**  
The smallest number in `nums` is `3`.
The largest number in `nums` is `8`.
The greatest common divisor of `3` and `8` is `1`.

### Example 3:
**Input:** `nums = [3,3]`  
**Output:** `3`  
**Explanation:**  
The smallest number in `nums` is `3`.
The largest number in `nums` is `3`.
The greatest common divisor of `3` and `3` is `3`.

### Constraints:
- `2 <= nums.length <= 1000`
- `1 <= nums[i] <= 1000`

---

## Solution
```java
import java.util.Arrays;

class Solution {
    public int findGCD(int[] nums) {
        Arrays.sort(nums);
        return hcf(nums[0], nums[nums.length - 1]);
    }

    public int hcf(int x, int y) {
        int dividend = Math.max(x, y);
        int divisor = Math.min(x, y);
        if (divisor == 0)
            return dividend;
        else if (divisor < 0)
            return divisor;
        else {
            while (divisor != 0) {
                int temp = divisor;
                divisor = dividend % divisor;
                dividend = temp;
            }
        }
        return dividend;
    }
}
```

## Explanation
1. **Sorting the Array:** The array is sorted to easily get the smallest and largest elements.
2. **Finding GCD:** The function `hcf(x, y)` calculates the greatest common divisor using the Euclidean algorithm.
3. **Euclidean Algorithm:**
   - Assign the larger number as `dividend` and the smaller number as `divisor`.
   - Apply modulo operation iteratively until the `divisor` becomes zero.
   - The last non-zero `dividend` is the greatest common divisor (GCD).

### Complexity Analysis
- **Sorting:** `O(n log n)`
- **GCD Calculation:** `O(log min(a, b))`
- **Overall Complexity:** `O(n log n)` (dominated by sorting)
