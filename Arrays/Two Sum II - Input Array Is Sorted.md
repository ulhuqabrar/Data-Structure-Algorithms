# Problem: Two Sum II - Input Array Is Sorted 🎯  
**Link:** [Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)  
**Difficulty:** Medium  
**Category:** Arrays  
**Topics:** Two-Pointer Technique, Binary Search  

---

## 📌 Problem Statement  
Given a **1-indexed sorted array** of integers `numbers`, find two numbers such that they add up to a specific target.  
Return their indices `[index1, index2]` (with `index1 < index2`), where both are **1-based indices**.  

- Each input has exactly **one solution**.  
- Cannot use the same element twice.  
- Must use **O(1) extra space**.  

---

## 🔎 Examples  

```cpp
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
// 2 + 7 = 9

Input: numbers = [2,3,4], target = 6
Output: [1,3]
// 2 + 4 = 6

Input: numbers = [-1,0], target = -1
Output: [1,2]
// -1 + 0 = -1
```
🛠️ Constraints

2 <= numbers.length <= 3 * 10^4

-1000 <= numbers[i] <= 1000

Array is sorted in non-decreasing order

-1000 <= target <= 1000

Exactly one solution guaranteed

💡 Approach (Two-Pointer)

Because the array is sorted, we can avoid brute force.

Steps:

Place one pointer at start (0) and another at end (n-1).

Compute sum = numbers[start] + numbers[end].

If sum == target: return indices (start+1, end+1) since indices are 1-based.

If sum < target: we need a larger sum, so move start++.

If sum > target: we need a smaller sum, so move end--.

Continue until a solution is found.

This works because the array is sorted → moving pointers guarantees progress towards the target.

🧩 Code Implementation
class Solution {
public:
    vector<int> twoSum(vector<int>& numbers, int target) {
        vector<int> ans;
        int start = 0, end = numbers.size() - 1;

        while (start < end) {
            int sum = numbers[start] + numbers[end];
            
            if (sum == target) {
                ans.push_back(start + 1); // +1 for 1-based index
                ans.push_back(end + 1);
                return ans;
            }
            else if (sum < target) {
                start++; // need bigger sum → move left pointer right
            }
            else {
                end--;   // need smaller sum → move right pointer left
            }
        }
        return ans; // not reached because one solution is guaranteed
    }
};

🖥️ Code Explanation (Line by Line)

    int start = 0, end = numbers.size()-1;

        Start pointer at first element, end pointer at last element.

    while (start < end)

        Keep looping until pointers cross.

    int sum = numbers[start] + numbers[end];

        Calculate the current sum.

    if (sum == target)

        Found the pair → return indices (converted to 1-based).

    else if (sum < target)

        Current sum is too small → shift start++ to increase it.

    else end--;

        Current sum is too big → shift end-- to decrease it.

✅ Example Run

For numbers = [2,7,11,15], target = 9:

    start=0 (2), end=3 (15) → sum=17 > 9 → move end → now end=2

    start=0 (2), end=2 (11) → sum=13 > 9 → move end → now end=1

    start=0 (2), end=1 (7) → sum=9 == target ✔ → return [1,2]

🔑 Key Takeaways

    Two-pointer technique saves space → O(1).

    Time Complexity: O(n)

    Space Complexity: O(1)

    Works only because the input array is sorted.
