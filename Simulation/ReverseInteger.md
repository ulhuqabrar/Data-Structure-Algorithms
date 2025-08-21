# Problem: Reverse Integer 🔄  
**Link:** [Reverse Integer (LeetCode #7)](https://leetcode.com/problems/reverse-integer/)  
**Difficulty:** Medium  
**Category:** Math  
**Topics:** Digit Manipulation, Overflow Handling  

---

##  Problem Statement  
Given a **signed 32-bit integer** `x`, return `x` with its digits reversed.  
If reversing `x` causes it to go outside the signed 32-bit range `[-2^31, 2^31 - 1]`, return **0**.  
Assume the environment does **not** support 64-bit integers.

---

##  Examples  

```cpp
Input: x = 123
Output: 321

Input: x = -123
Output: -321

Input: x = 120
Output: 21
```
Constraints

    -2^31 <= x <= 2^31 - 1

    Can't use 64-bit arithmetic — must handle overflow with checks.

Approach (Digit-by-Digit Reversal + Overflow Check)

We reverse the integer one digit at a time using % and /, while managing overflow using safe boundary checks:

Steps:

    Initialize ans = 0.

    While x != 0, extract the last digit rem = x % 10, then truncate x /= 10.

    Before appending digit, check if ans will overflow when multiplied by 10 and added with rem.

    If overflow would occur → return 0.

    Otherwise, update ans = ans * 10 + rem.

    Repeat until all digits are reversed.

    Return the final ans.

Code Implementation

class Solution {
public:
    int reverse(int x) {
        int ans = 0, rem;

        while (x != 0) {
            rem = x % 10;
            x /= 10;

            // Check for overflow before we multiply by 10 and add rem
            if (ans > INT_MAX / 10 || (ans == INT_MAX / 10 && rem > 7)) return 0;
            if (ans < INT_MIN / 10 || (ans == INT_MIN / 10 && rem < -8)) return 0;

            ans = ans * 10 + rem;
        }

        return ans;
    }
};

Code Explanation (Line by Line)

    int ans = 0, rem;

        ans stores the reversed result; rem holds the current digit.

    while (x != 0)

        Keep extracting digits until x becomes zero.

    rem = x % 10; x /= 10;

        rem: last digit; then remove it from x.

    Overflow Checks

        ans > INT_MAX / 10 means ans * 10 alone would overflow.

        If ans == INT_MAX / 10, then adding rem > 7 (i.e., > last digit of INT_MAX) overflows.

        Similarly for negative range with INT_MIN.

    ans = ans * 10 + rem;

        Safely append the digit.

    return ans;

        Final reversed integer (or 0 if overflow occurred).

Example Walkthrough

    Input: x = 123

        rem = 3, ans = 3

        rem = 2, ans = 32

        rem = 1, ans = 321 → Return 321

    Input: x = -123

        rem = -3, ans = -3

        rem = -2, ans = -32

        rem = -1, ans = -321 → Return -321

    Edge Cases:

        Large inputs like 1534236469:

            Detect overflow during processing → return 0

Key Takeaways

    Digit-by-digit reversal helps avoid complex operations.

    Overflow handling is essential—can't use 64-bit types here.

    Time Complexity: O(d), where d = number of digits (~10 for 32-bit).

    Space Complexity: O(1).
