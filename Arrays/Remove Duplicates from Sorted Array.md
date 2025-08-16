# 26. Remove Duplicates from Sorted Array 🚀  

**Link:** [LeetCode Problem](https://leetcode.com/problems/remove-duplicates-from-sorted-array/)  
**Difficulty:** Easy  
**Category:** Arrays  
**Topics:** Two-Pointer Technique, In-place Modification  

---

## 📌 Problem Statement  
Given an integer array `nums` sorted in **non-decreasing order**, remove the duplicates **in-place** such that each unique element appears only once.  

- The **relative order** of elements must be preserved.  
- Return the number of unique elements `k`.  

The judge checks if:  
- First `k` elements in `nums` are unique and in correct order.  
- The rest of the array can be ignored.  

---

## 🔍 Examples  

### Example 1  
**Input:** `nums = [1,1,2]`  
**Output:** `2, nums = [1,2,_]`  
**Explanation:** First two elements are `[1,2]`.  

---

### Example 2  
**Input:** `nums = [0,0,1,1,1,2,2,3,3,4]`  
**Output:** `5, nums = [0,1,2,3,4,_,_,_,_,_]`  
**Explanation:** First five elements are `[0,1,2,3,4]`.  

---

## 🛠️ Constraints  
- `1 <= nums.length <= 3 * 10^4`  
- `-100 <= nums[i] <= 100`  
- `nums` is sorted in non-decreasing order  

---

## 💡 Approach  

Since the array is **sorted**, duplicates will always be next to each other.  
We can use a **two-pointer technique**:  

1. Use a pointer `count` to track the position of the next unique element.  
2. Start with `count = 1` (since the first element is always unique).  
3. Traverse from index `1` to `n-1`:  
   - If `nums[i] != nums[i-1]`, it's a unique element.  
   - Place it at `nums[count]` and increment `count`.  
4. Return `count`.  

This ensures all unique elements are placed at the front.  

---

## 🧩 Code Implementation  

```cpp
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int count = 1; // First element is always unique

        for (int i = 1; i < nums.size(); i++) {
            if (nums[i] != nums[i - 1]) {
                nums[count] = nums[i]; // Place unique element
                count++;
            }
        }
        return count; // Number of unique elements
    }
};
```

✅ Example Walkthrough

For nums = [0,0,1,1,1,2,2,3,3,4]

    Start: count = 1

    i=1: nums[1] == nums[0] → skip

    i=2: nums[2] != nums[1] → place 1 at nums[1] → count=2

    i=3: nums[3] == nums[2] → skip

    i=5: nums[5] != nums[4] → place 2 at nums[2] → count=3

    Continue…

Final nums = [0,1,2,3,4,...], return 5.
🔑 Key Takeaways

    Two-pointer approach ensures in-place operation.

    Time Complexity: O(n)

    Space Complexity: O(1)

    Good example of in-place modification + array traversal problems.
