## Summary
- When we need to look for something, binary search on a sorted array is a substitution of hashmap. It takes a little longer time, and uses O(1) space.

## Clarify
- The array is sorted
- must have one solution?
- Can target be negative?
- what's the order of num1 and num2?

## Solution 1
### Keyword:
Hashtable
### Analysis:
Using Hashtable doesn't require the array to be sorted. In that case, we just need to look for both num+target and num-target . However, it takes O(n) space. So when the amount of input is huge and cannot be put into memory, we have to use the following ways.
### Complexity:
TC: O(n) SC:O(n)
### Code:
```py
def two_sum7(self, nums: List[int], target: int) -> List[int]:
        # write your code here
        visited = set()
        target = abs(target)
        for num in nums:
            if num - target in visited:
                return [num - target, num]
            visited.add(num)
```

## Solution 2:
### Keyword:
Binary search
### Analysis:
For each number, we use binary search to look for its pair.
### Complexity:
TC: O(NlogN) SC:O(1)
### Code:
```py
class Solution:
    """
    @param nums: an array of Integer
    @param target: an integer
    @return: [num1, num2] (index1 < index2)
    """
    def two_sum7(self, nums: List[int], target: int) -> List[int]:
        # write your code here
        target = abs(target)
        for i in range(len(nums)):
            idx = self.binary_search(nums, i + 1, len(nums) - 1, nums[i] + target)
            if idx != -1:
                return [nums[i], nums[idx]]

    def binary_search(self, nums, start, end, target):
        while start + 1 < end:
            mid = (start + end) // 2
            if nums[mid] == target:
                return mid
            elif nums[mid] < target:
                start = mid
            else:
                end = mid
        if nums[start] == target: return start
        if nums[end] == target: return end
        return -1
```

## Solution 3:
### Keyword:
Two pointers
### Analysis:

### Complexity:
TC: O(N) SC:O(1)
### Code:
```py
def two_sum7(self, nums: List[int], target: int) -> List[int]:
    # write your code here
    n = len(nums)
    j = 1
    target = abs(target)
    for i in range(n):
        j = max(i + 1, j)  # [0,1,3] 0 
        while j < n and nums[j] - nums[i] < target:
            j += 1
        if j == n:
            break
        if nums[j] - nums[i] == target:
            return [nums[i], nums[j]]
    return [-1, -1]
```
