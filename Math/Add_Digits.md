# Problem: Add Digits 📱  
**Link:** [Add Digits (LeetCode #258)](https://leetcode.com/problems/add-digits/)  
**Difficulty:** Easy  
**Category:** Math  
**Topics:** Digit Manipulation, Looping, In-Place Reduction  

---

##  ​ Problem Statement  
Given an integer `num`, **repeatedly** add all its digits until the result has **only one digit**, then return that one-digit result.

---

##  ​ Examples  

```cpp
Input: num = 38
Output: 2
Explanation:
38 → 3 + 8 = 11
11 → 1 + 1 = 2
Result = 2 (a single digit)

Input: num = 0
Output: 0
```
Constraints

    0 <= num <= 2^31 - 1

Approach (Iterative Digit Sum)

We can repeatedly reduce the number by summing its digits until it's a single-digit number:

Steps:

    While num > 9, do:

        Initialize a sum = 0.

        Extract each digit using repeated % 10 and /= 10, accumulating into sum.

        After digit summing, set num = sum and repeat.

    Once num <= 9, return num.

This brute-force technique works effectively within the input constraint range using O(log n) operations per sum.

(Optional note for future-you: there's a constant-time math trick—the digit root formula—but this iterative method is more intuitive for initial learning.)
Code Implementation

class Solution {
public:
    int addDigits(int num) {
        // Continue until 'num' becomes a single-digit number
        while (num > 9) {
            int sum = 0;      // Accumulate sum of digits
            while (num != 0) {
                sum += num % 10;  // Add least significant digit
                num /= 10;        // Remove that digit
            }
            num = sum;  // Reduce 'num' to its digit sum
        }
        return num;      // Final one-digit result
    }
};

𝖢𝗈𝖽𝖾 𝖤𝖷𝗉𝗅𝖺𝗇𝖺𝗍𝗂𝗈𝗇 (Line by Line)

    while (num > 9)

        Keep looping until num has more than one digit.

    int sum = 0;

        Initialize a variable to accumulate digit sums.

    while (num != 0)

        Extract digits from right to left:

            sum += num % 10; → capture the last digit.

            num /= 10; → remove the last digit.

    num = sum;

        Collapse all digits into num and repeat if needed.

    return num;

        Finally return the single-digit result.

Example Walkthrough

For num = 38:

    First pass: 3 + 8 = 11

    Next: 1 + 1 = 2

    Return 2 because it's a single digit.

For num = 0:

    0 is already a single digit → return 0.

𝖪𝖾𝗒 𝖳𝖺𝗄𝖾𝖺𝗐𝗌

    Straight-forward digit summing loops reduce number gradually.

    Time Complexity: O(log n) — digit operations based on number length.

    Space Complexity: O(1) — fixed variables only.

    Great for understanding number manipulation basics.

    There's an alternative digit-root formula method (1 + (n - 1) % 9), which is faster but less intuitive early on.
