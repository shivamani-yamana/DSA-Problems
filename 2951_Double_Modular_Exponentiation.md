# 2961. Double Modular Exponentiation
**Difficulty**: Medium  
**Algorithm**: Modular Exponentiation

## Problem Description

You are given a 0-indexed 2D array `variables` where `variables[i] = [ai, bi, ci, mi]`, and an integer `target`.

An index `i` is good if the following formula holds:

```
0 <= i < variables.length
((a^b % 10)^c) % m == target
```

Return an array consisting of good indices in any order.

### Example 1:
**Input**:  
`variables = [[2,3,3,10],[3,3,3,1],[6,1,1,4]], target = 2`  
**Output**:  
`[0,2]`

**Explanation**:  
For each index `i` in the `variables` array:
1) For the index 0, `variables[0] = [2,3,3,10]`, `(2^3 % 10)^3 % 10 = 2`.
2) For the index 1, `variables[1] = [3,3,3,1]`, `(3^3 % 10)^3 % 1 = 0`.
3) For the index 2, `variables[2] = [6,1,1,4]`, `(6^1 % 10)^1 % 4 = 2`.

Therefore, we return `[0,2]` as the answer.

### Example 2:
**Input**:  
`variables = [[39,3,1000,1000]], target = 17`  
**Output**:  
`[]`

**Explanation**:  
For the index 0, `variables[0] = [39,3,1000,1000]`, `(39^3 % 10)^1000 % 1000 = 1`.

Therefore, we return `[]` as the answer.

## Constraints:
- `1 <= variables.length <= 100`
- `variables[i] == [ai, bi, ci, mi]`
- `1 <= ai, bi, ci, mi <= 10^3`
- `0 <= target <= 10^3`

## Solution

```java
class Solution {
    public List<Integer> getGoodIndices(int[][] variables, int target) {
        List<Integer> result = new ArrayList<Integer>();
        for(int i = 0; i < variables.length; i++) {
            int[] variable = variables[i];
            int pow1 = powMod(variable[0], variable[1], 10);
            int pow2 = powMod(pow1, variable[2], variable[3]);
            if(pow2 == target) {
                result.add(i);
            }
        }
        return result;
    }

    public int powMod(int base, int exp, int mod) {
        if (exp == 0) return 1;
        int half = powMod(base, exp / 2, mod);
        if (exp % 2 == 0) return half * half % mod;
        else return base * half * half % mod;
    }
}
```

## Explanation
We need to check each index `i` in the `variables` array for whether the formula `((a^b % 10)^c) % m == target` holds. To do this, we calculate `a^b % 10` using modular exponentiation. Then, we calculate `((a^b % 10)^c) % m`. If the result equals the `target`, we add the index `i` to the result list.

### Time Complexity:
The time complexity is `O(n * log(max(exp)))`, where `n` is the length of the `variables` array and `max(exp)` is the maximum exponent in the `variables` array, since we use the modular exponentiation algorithm which has a time complexity of `O(log(exp))`.

### Space Complexity:
The space complexity is `O(n)` for the result list.
```
