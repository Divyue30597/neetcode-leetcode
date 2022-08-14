```
Given an array of strings strs, group the anagrams together. You can return the answer in any order.
An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.

Example 1:
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Example 2:
Input: strs = [""]
Output: [[""]]

Example 3:
Input: strs = ["a"]
Output: [["a"]]

Constraints:
    1 <= strs.length <= 104
    0 <= strs[i].length <= 100
    strs[i] consists of lowercase English letters.
```

```go
func groupAnagrams(strs []string) [][]string {
    var res = map[[26]int][]string{}
    
    // Here we are looping over the array strs
    for _, str := range strs {
        count := [26]int{}
        // Here we are looping over each string present in the array
        for i:=0 ; i < len(str); i++ {
            // since count's len is 26 and 'a' represents the rune/uint32 and 'a' -> its value will be taken as ascii value.
            count[str[i]-'a'] += 1
        }
        // adding the key count to our map and appending that str as the value 
        res[count] = append(res[count], str)
    }
    resOp := [][]string{} 
    for _, val := range res {
        resOp = append(resOp, val)
    }
    return resOp
}
```

```
Given an integer array nums and an integer k, return the k most frequent elements. You may return the answer in any order.

Example 1:
Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]

Example 2:
Input: nums = [1], k = 1
Output: [1]

Constraints:
    1 <= nums.length <= 105
    -104 <= nums[i] <= 104
    k is in the range [1, the number of unique elements in the array].
    It is guaranteed that the answer is unique.

Follow up: Your algorithm's time complexity must be better than O(n log n), where n is the array's size.
```

```go
func topKFrequent(nums []int, k int) []int {
	// no of times the num is repeating
	freq := make([][]int, len(nums)+1)
	// keeping track of the count -> no of times the item appears.
	count := make(map[int]int)
	// Resultant array with k as length
	result := make([]int, 0)

	// looping through nums array and we are using value of input array as key for the count and increasing it's value each time.
	for _, num := range nums {
		// Creating hashmap with input array val
		// {"1": 3, "2": 2, "3": 1}
		count[num]++
	}

	// looping over the count with the key, val, keeping the value 'c' here as the index of the freq array and appending the num as to that index.
	for num, c := range count {
		// len(freq) = 7 [0...7]
		// [[],[3],[2],[1],[],[],[]]
		freq[c] = append(freq[c], num)
	}

	// Now we have to get the k elements from the count
	// [[],[3],[2],[1],[],[],[]] -> loop over this array
	for i := len(freq) - 1; i >= 0; i-- {
		// here, val = item in the freq array.
		for _, val := range freq[i] {
            result = append(result, val)
			if len(result) == k {
				return result
			}
		}
	}
	return result
}
```

```
Given an integer array nums, return an array answer such that answer[i] is equal to the product of all the elements of nums except nums[i].

The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.

You must write an algorithm that runs in O(n) time and without using the division operation.

Example 1:
Input: nums = [1,2,3,4]
Output: [24,12,8,6]

Example 2:
Input: nums = [-1,1,0,-3,3]
Output: [0,0,9,0,0]

Constraints:
  2 <= nums.length <= 105
  -30 <= nums[i] <= 30
  The product of any prefix or suffix of nums is guaranteed to fit in a 32-bit integer.
```


```go
func productExceptSelf(nums []int) []int {
    // Initializing the prefix, postfix and result
    prefix := 1
    postfix := 1
    result := make([]int, len(nums))
    // looping over the nums input array
    for index, _ := range nums {
        // starting with storing the prefix value as result's array first val
        result[index] = prefix
        // Updating the value of the prefix with each iteration
        prefix *= nums[index]
    }
    // applying the postfix logic
    for i:= len(nums) -1; i >= 0; i-- {
        // updating the last val of the result by multiplying it with the default postfix val
        // and the with each iteration we update the result array value and the postfix value
        result[i] *= postfix
        postfix *= nums[i]
    }
    return result
}
```