```
Given a 1-indexed array of integers numbers that is already sorted in non-decreasing order, find two numbers such that they add up to a specific target number. Let these two numbers be numbers[index1] and numbers[index2] where 1 <= index1 < index2 <= numbers.length.

Return the indices of the two numbers, index1 and index2, added by one as an integer array [index1, index2] of length 2.

The tests are generated such that there is exactly one solution. You may not use the same element twice.

Your solution must use only constant extra space.

Example 1:
Input: numbers = [2,7,11,15], target = 9
Output: [1,2]
Explanation: The sum of 2 and 7 is 9. Therefore, index1 = 1, index2 = 2. We return [1, 2].

Example 2:
Input: numbers = [2,3,4], target = 6
Output: [1,3]
Explanation: The sum of 2 and 4 is 6. Therefore index1 = 1, index2 = 3. We return [1, 3].

Example 3:
Input: numbers = [-1,0], target = -1
Output: [1,2]
Explanation: The sum of -1 and 0 is -1. Therefore index1 = 1, index2 = 2. We return [1, 2].

Constraints:

    2 <= numbers.length <= 3 * 104
    -1000 <= numbers[i] <= 1000
    numbers is sorted in non-decreasing order.
    -1000 <= target <= 1000
    The tests are generated such that there is exactly one solution.
```
```go
func twoSum(numbers []int, target int) []int {
    leftPointer, rightPointer := 0, len(numbers)-1
    
    for leftPointer < rightPointer {
        var currSum int = numbers[rightPointer] + numbers[leftPointer]
        
        if currSum > target {
            rightPointer--
        } else if currSum < target {
            leftPointer++            
        } else {
            return []int{leftPointer+1,rightPointer+1}
        }
    }
    return nil
}
```

```
Given an integer array nums, return all the triplets [nums[i], nums[j], nums[k]] such that i != j, i != k, and j != k, and nums[i] + nums[j] + nums[k] == 0.

Notice that the solution set must not contain duplicate triplets.

Example 1:

Input: nums = [-1,0,1,2,-1,-4]
Output: [[-1,-1,2],[-1,0,1]]
Explanation:
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.

Example 2:
Input: nums = [0,1,1]
Output: []
Explanation: The only possible triplet does not sum up to 0.

Example 3:
Input: nums = [0,0,0]
Output: [[0,0,0]]
Explanation: The only possible triplet sums up to 0.

Constraints:
    3 <= nums.length <= 3000
    -10^5 <= nums[i] <= 10^5
```

### Solution

Time Complexity: O(n).O(n.log(n)) = O(n^2)

```go
func threeSum(nums []int) [][]int {
    result := [][]int{}

    sort.Ints(nums)

    for i:=0 ; i < len(nums); i++ {

        // After sorting if we get the same value then we need to continue
        // in this case, [-4,-1,-1,0,1,2] -> [-1, -1]
        if i > 0 && nums[i] == nums[i-1] {
            continue
        }

        // Starting the twoSum - 2 algo here with two pointers
        leftPointer := i+1
        rightPointer := len(nums)-1

        for leftPointer < rightPointer {
            threeSum := nums[i] + nums[leftPointer] + nums[rightPointer]

            if threeSum > 0 {
                rightPointer -= 1
            } else if threeSum < 0 {
                leftPointer += 1
            } else {
                result = append(result, []int{nums[i], nums[leftPointer], nums[rightPointer]})
                leftPointer += 1
                // We are checking if the leftPointer and the value before it is same.
                for nums[leftPointer] == nums[leftPointer - 1] && leftPointer < rightPointer {
                    leftPointer += 1
                }
            }
        }
    }
    return result
}
```
