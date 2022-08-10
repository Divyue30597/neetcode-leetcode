```
Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.
You must write an algorithm with O(log n) runtime complexity.

Example 1:
Input: nums = [-1,0,3,5,9,12], target = 9
Output: 4
Explanation: 9 exists in nums and its index is 4

Example 2:
Input: nums = [-1,0,3,5,9,12], target = 2
Output: -1
Explanation: 2 does not exist in nums so return -1
```

### Solution

One of the solution is to loop over the array and compare it.

Time Complexity: O(n)

```go
func search(nums []int, target int) int {
    for i:=0; i<len(nums); i++ {
        if nums[i]==target {
            return i
        }
    }
    return -1
}
```

Other solution is using Binary Search.

```go
func search(nums []int, target int) int {
    for leftPointer,rightPointer:= 0, len(nums)-1; leftPointer<=rightPointer ; {
        // midPointer := (leftPointer + rightPointer)/2
        midPointer := leftPointer + (rightPointer - leftPointer) / 2
        if nums[midPointer] > target {
            rightPointer = midPointer - 1
        } else if nums[midPointer] < target {
            leftPointer = midPointer + 1
        } else {
            return midPointer
        }
    }
    return -1
}
```

```
Given the head of a singly linked list, reverse the list, and return the reversed list.

Example 1:
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]

Example 2:
Input: head = [1,2]
Output: [2,1]

Example 3:
Input: head = []
Output: []

Input : 1 -> 2 -> 3 -> 4 -> 5 -> nil

Output : 5 -> 4 -> 3 -> 2 -> 1 -> nil

Constraints:
    The number of nodes in the list is the range [0, 5000].
    -5000 <= Node.val <= 5000
```

Can be done iteratively

```
Using 2 pointers curr and prev

initialize curr to nil and prev to head
1.    curr.Next
      ⬇️
      1 -> 2 -> 3 -> nil
⬆️   ⬆️
prev  curr

We will point the prev to curr now and curr.Next to prev and curr to curr.Next
2.
nil<- 1 ->    2     -> 3 -> nil
      ⬆️     ⬇️
prev->curr->curr.Next

So, it will be something like this,

nil<- 1 ->    2     -> 3 -> nil
      ⬆️     ⬆️
      prev    curr

Now, same thing assign curr.Next to prev, prev -> curr, curr -> curr.Next
PS Store the value of curr.Next in temp variable.
            prev <- curr.Next
            ⬇️   ⬇️
nil <- 1 <- 2  -> 3 -> nil
            ⬆️   ⬆️
            prev  curr
```

```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseList(head *ListNode) *ListNode {
    var prev *ListNode
    curr := head

    for curr != nil {
        temp := curr.Next
        curr.Next = prev
        prev = curr
        curr = temp
    }
    return prev
}
```
