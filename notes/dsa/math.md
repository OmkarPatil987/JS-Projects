### **Problem 1: Check if a Number is a Palindrome**

**What is the Problem?**  
We need to determine if a number reads the same forwards and backwards (e.g., 121 is the same as 121, but 123 is not 321).

**Why Solve It?**  
Palindromes are common in problems involving symmetry, such as string or number validation, pattern recognition, or data integrity checks. Solving without string conversion is efficient for numerical inputs.

**First Principles Derivation:**

- A number is palindromic if its digits, read left-to-right, match right-to-left.
- From first principles, we can extract digits using division and modulo (base-10 system).
- To avoid strings, we reverse the number mathematically by rebuilding it digit-by-digit.
- Key question: How do we get digits? Use modulo 10 to get the last digit and integer division by 10 to remove it.
- Build the reversed number by multiplying by 10 and adding digits.
- Compare the original and reversed numbers.

**Solution:**

```javascript
function isPalindrome(n) {
    if (n < 0) return false; // Negative numbers can't be palindromes
    let original = n, reversed = 0;
    while (n > 0) {
        let digit = n % 10; // Extract last digit
        reversed = reversed * 10 + digit; // Build reversed number
        n = Math.floor(n / 10); // Remove last digit
    }
    return original === reversed;
}
```

**Example:**

- Input: 121 → reversed = 121 → Output: `true`
- Input: -121 → Output: `false` (negative)
- Input: 123 → reversed = 321 → Output: `false`

**Edge Cases:**

- Negative numbers (not palindromes).
- Single digits (always palindromes).
- Zero (palindrome).