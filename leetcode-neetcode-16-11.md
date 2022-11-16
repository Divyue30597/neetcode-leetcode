```
Given a string s consisting of words and spaces, return the length of the last word in the string.
A word is a maximal substring consisting of non-space characters only.

Example 1:
Input: s = "Hello World"
Output: 5
Explanation: The last word is "World" with length 5.

Example 2:
Input: s = "   fly me   to   the moon  "
Output: 4
Explanation: The last word is "moon" with length 4.

Example 3:
Input: s = "luffy is still joyboy"
Output: 6
Explanation: The last word is "joyboy" with length 6.


Constraints:
1 <= s.length <= 104
s consists of only English letters and spaces ' '.
There will be at least one word in s.
```

## Solution

- We can loop the string from the end.
- Look for the space and reduce the len of the string
- Initialize a counter for every non-space character

## Using go inbuilt library strings

```go
func lengthOfLastWord(s string) int {
    str:= strings.Fields(s)
    return len(str[len(str)-1])
}
```

## Using algo

```go
func lengthOfLastWord(s string) int {
    count := 0

    for i:=len(s)-1; i >= 0; i-- {
        if count == 0 && s[i]==' ' {
            continue
        } else {
            if s[i] == ' ' {
                    break
            }
                count++
        }
    }
    return count
}
```

```
Write a function to find the longest common prefix string amongst an array of strings.
If there is no common prefix, return an empty string "".

Example 1:
Input: strs = ["flower","flow","flight"]
Output: "fl"

Example 2:
Input: strs = ["dog","racecar","car"]
Output: ""

Explanation: There is no common prefix among the input strings.

Constraints:
1 <= strs.length <= 200
0 <= strs[i].length <= 200
strs[i] consists of only lowercase English letters.
```

```go
func longestCommonPrefix(strs []string) string {
    res:=""

    // comparing with the first string present in the array
    // taking the length of the first elem into account
    for i:=0; i < len(strs[0]); i++ {
        // looping over the whole array and then comparing the first elem of each string
        for str:=0; str<len(strs); str++ {
            // comparing the strings character with the first if they dont match then we return the res
            if i == len(strs[str]) || strs[str][i] != strs[0][i] {
                return res
            }
        }
        // storing the char which are similar in the res
        res += string(strs[0][i])
    }

    return res
}
```
