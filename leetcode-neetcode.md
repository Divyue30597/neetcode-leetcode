# Leetcode - neetcode

[neetcode](https://neetcode.io/)

## Arrays and Hashing

### 1. Contains Duplicate

```
Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.

Example 1:
Input: nums = [1,2,3,1]
Output: true

Example 2:
Input: nums = [1,2,3,4]
Output: false

Example 3:
Input: nums = [1,1,1,3,3,4,3,2,4,2]
Output: true
```

Three approaches can be applied here.

1. Using Brute force  
   Space complexity : O(1)  
   Time Complexity : O(n^2)
2. Using Sorting  
   Space complexity : O(1)  
   Time Complexity : O(n\*log(n))
3. Using Hashmap -> Best approach  
   Space complexity : O(n)  
   Time Complexity : O(n)

_*While using hashmap we have to compromise with the space.*_

```go
func containsDuplicate(nums []int) bool {
    hashMap := make(map[int]bool)

    for _, num := range nums {
        if hashMap[num] {
            return true
        } else {
            hashMap[num] = true
        }
    }
    return false
}
```

### 2. Valid Anagram

```
Given two strings s and t, return true if t is an anagram of s, and false otherwise.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:
Input: s = "anagram", t = "nagaram"
Output: true

Example 2:
Input: s = "rat", t = "car"
Output: false

Constraints:
    1 <= s.length, t.length <= 5 * 104
    s and t consist of lowercase English letters.
```

Here 2 approaches can be followed:

1. Creating the hashmap of both the string and then comparing the
   number of time each letter is repeated.
2. We can sort the string and then try to compare the string directly
   if they are equal to each other.

```go
func isAnagram(s string, t string) bool {
    CountS, CountT := make(map[string]int), make(map[string]int)
    if len(s) != len(t) {
        return false
    }

    for i:=0; i<len(s); i++ {
        CountS[string(s[i])] += 1
        CountT[string(t[i])] += 1
    }

    for i:=0; i<len(s); i++ {
        if CountS[string(s[i])] != CountT[string(s[i])] {
            return false
        }
    }
    return true
}
```

### 3. Two Sum

```
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

You can return the answer in any order.

Example 1:
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Explanation: Because nums[0] + nums[1] == 9, we return [0, 1].

Example 2:
Input: nums = [3,2,4], target = 6
Output: [1,2]

Example 3:
Input: nums = [3,3], target = 6
Output: [0,1]
```

Two ways to solve this problem is using Brute force and Using hashMap.

Below is done using HashMap.

```go
func twoSum(nums []int, target int) []int {
    hashMap := make(map[int]int)

    for currIndex, currVal := range nums {
        // using comma, ok syntax
        if requiredIndex, isPresent := hashMap[target-currVal]; isPresent {
            return []int{requiredIndex, currIndex}
        }
        hashMap[currVal] = currIndex
    }
    return []int{}
}
```
