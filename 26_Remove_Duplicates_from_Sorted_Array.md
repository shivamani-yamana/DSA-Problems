# 26. Remove Duplicates from Sorted Array (EASY)

## Problem Statement
Given an integer array `nums` sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same. Then return the number of unique elements in `nums`.

Consider the number of unique elements of `nums` to be `k`. To get accepted, you need to do the following:
- Modify the array `nums` such that the first `k` elements contain the unique elements in order.
- Return `k`.

### Example 1:
**Input:** `nums = [1,1,2]`  
**Output:** `2, nums = [1,2,_]`  
**Explanation:**  
Your function should return `k = 2`, with the first two elements being `1` and `2`. It does not matter what remains beyond `k`.

### Example 2:
**Input:** `nums = [0,0,1,1,1,2,2,3,3,4]`  
**Output:** `5, nums = [0,1,2,3,4,_,_,_,_,_]`  
**Explanation:**  
Your function should return `k = 5`, with the first five elements being `0, 1, 2, 3, and 4`.

### Constraints:
- `1 <= nums.length <= 3 * 10^4`
- `-100 <= nums[i] <= 100`
- `nums` is sorted in non-decreasing order.

---

## Solution
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 1) return 1;
        int start = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] == nums[i - 1]) continue;
            nums[start] = nums[i];
            start++;
        }
        return start;
    }
}
```

## Explanation
1. **Edge Case Handling:** If the array has only one element, return `1` directly.
2. **Using Two Pointers:**
   - `start` is used to track the position where the next unique element should be placed.
   - Iterate through the array, and when encountering a new element (not equal to the previous one), update `nums[start]`.
3. **Return `start`:** It represents the count of unique elements.

### Complexity Analysis
- **Time Complexity:** `O(n)`, where `n` is the length of `nums`, since we traverse the array once.
- **Space Complexity:** `O(1)`, as we modify the input array in place without extra space.
