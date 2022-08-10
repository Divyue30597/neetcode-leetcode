# Leetcode - neetcode

[neetcode](https://neetcode.io/)

## Pointers

### Valid Palindrome

```
A phrase is a palindrome if, after converting all uppercase letters into lowercase letters and removing all non-alphanumeric characters, it reads the same forward and backward. Alphanumeric characters include letters and numbers.

Given a string s, return true if it is a palindrome, or false otherwise.

Example 1:
Input: s = "A man, a plan, a canal: Panama"
Output: true
Explanation: "amanaplanacanalpanama" is a palindrome.

Example 2:
Input: s = "race a car"
Output: false
Explanation: "raceacar" is not a palindrome.

Example 3:
Input: s = " "
Output: true
Explanation: s is an empty string "" after removing non-alphanumeric characters.
Since an empty string reads the same forward and backward, it is a palindrome.

Constraints:
    1 <= s.length <= 2 * 105
    s consists only of printable ASCII characters.
```

#### Solution:

1. Removing all the unwanted things which are not alphanumeric and then looping  
   over them and considering it is a palindrone both the input and reversed result  
   will be the same.

2. Using pointers (not in terms of computer science), basically comparing the left most  
   and the right most value if they are same then return true. Increase the value by  
   incrmenting the value and decrease the left most value.

```go
func isPalindrome(s string) bool {
    for i, j:= 0, len(s)-1; i < j ; {
        leftPointer := s[i]
        rightPointer := s[j]

        if !isValidChar(leftPointer) {
            i++
            continue
        }

        if !isValidChar(rightPointer) {
            j--
            continue
        }

        if strings.ToLower(string(leftPointer)) != strings.ToLower(string(rightPointer)) {
            return false
        }
        i++
        j--
    }
    return true
}

func isValidChar(strUintVal byte) bool {
    return (strUintVal >= 65 && strUintVal <=90) || (strUintVal >=97  && strUintVal <= 122) || (strUintVal >= 48 && strUintVal <= 57)
}
```

## Best time to buy and sell stocks

```
You are given an array prices where prices[i] is the price of a given stock on the ith day.

You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

Example 1:
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

Example 2:
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```

### Solution

This can be done by using two pointers one at the end of the string and  
one at the starting. Thus for every small number than that of the previous  
one we need to update the leftpointer since we will buy at that point.   
The rightPointer is updated when we have a huge profit which can be calculated   
by using the leftpointer and the rightPointer places in the array. 

Time Complexity : O(n)
Space Complexity : O(1)

```go
func maxProfit(prices []int) int {
    if len(prices) <= 1 {
        return 0
    }
    var maxProfit float64
    for leftPointer, rightPointer := 0, 1; rightPointer < len(prices); {
        // leftPointer represents to buy
        // rightPointer represents to sell
        if prices[leftPointer] < prices[rightPointer] {
            var profit int = prices[rightPointer] - prices[leftPointer]
            maxProfit = math.Max(maxProfit, float64(profit))
        } else {
            leftPointer = rightPointer
        }
        rightPointer++
    }

    return int(maxProfit)
}
```

## Valid Parentheses

```
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:
    Open brackets must be closed by the same type of brackets.
    Open brackets must be closed in the correct order.

Example 1:
Input: s = "()"
Output: true

Example 2:
Input: s = "()[]{}"
Output: true

Example 3:
Input: s = "(]"
Output: false
```

### Solution:

This is solved using stack. For each opening brace we are pushing it inside the stack.  
For each closing bracket we are reducing the length of stack by one. returning if the   
len(stack) is equal to 0, then return true or else return false.

Time Complexity: O(n)
Space Complexity: O(1)

```go
func isValid(s string) bool {
   var stack []byte
    for _, c := range s {
        if c == '(' {
            stack = append(stack, ')')
        } else if c == '{' {
            stack = append(stack, '}')
        } else if c == '[' {
            stack = append(stack, ']')
        } else if len(stack) == 0 || stack[len(stack)-1] != byte(c) {
            return false
        } else {
            stack = stack[0:len(stack)-1]
        }
    }
    return len(stack) == 0
}
```


