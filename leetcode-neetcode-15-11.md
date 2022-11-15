```
Given an array arr, replace every element in that array with the greatest element among the elements to its right, and replace the last element with -1.

After doing so, return the array.

Example 1:

Input: arr = [17,18,5,4,6,1]
Output: [18,6,6,6,1,-1]
Explanation:
- index 0 --> the greatest element to the right of index 0 is index 1 (18).
- index 1 --> the greatest element to the right of index 1 is index 4 (6).
- index 2 --> the greatest element to the right of index 2 is index 4 (6).
- index 3 --> the greatest element to the right of index 3 is index 4 (6).
- index 4 --> the greatest element to the right of index 4 is index 5 (1).
- index 5 --> there are no elements to the right of index 5, so we put -1.

Example 2:

Input: arr = [400]
Output: [-1]
Explanation: There are no elements to the right of index 0.


Constraints:

1 <= arr.length <= 104
1 <= arr[i] <= 10
```

```go
func replaceElements(arr []int) []int {
    max := -1

    for i:= len(arr) -1; i >= 0; i-- {
        if arr[i] > max {
            arr[i], max = max, arr[i]
        } else {
            arr[i] = max
        }
    }

    return arr
}
```

Time Complexity: O(n)

```
Given two strings s and t, return true if s is a subsequence of t, or false otherwise.

A subsequence of a string is a new string that is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (i.e., "ace" is a subsequence of "abcde" while "aec" is not).

Example 1:
Input: s = "abc", t = "ahbgdc"
Output:

Example 2:
Input: s = "axc", t = "ahbgdc"
Output: false

Constraints:
0 <= s.length <= 100
0 <= t.length <= 104
s and t consist only of lowercase English letters.
```

Time Complexity: O(n)

```go
func isSubsequence(s string, t string) bool {
    // Initialize two pointers for each string
    ptrForS := 0
    ptrForT:= 0

    // initialize a loop for condition always being true
    for ptrForS < len(s) && ptrForT < len(t) {
        if s[ptrForS] == t[ptrForT] {
            // increase ptrForS if both strings character matches.
            ptrForS++
        }
        // always increase the ptrForT
        ptrForT++
    }
    // return here
    return ptrForS == len(s)
}
```
