## 解法1: 双指针 + Hashmap 
TC:O(N) SC:O(N)
```
class Solution:
    """
    @param nums: an array of integers
    @return: the number of unique integers
    """
    def deduplication(self, nums):
        # write your code here
        left, right = 0, 0
        visited = set()
        while right < len(nums):
            if nums[right] not in visited:
                nums[left] = nums[right]
                visited.add(nums[right])
                left += 1
            right += 1
        return left
```
## 解法2: 双指针 + Sort
TC:O(NlogN) SC:O(1)
同leetcode26. Remove Duplicates from Sorted Array
```
class Solution:
    """
    @param nums: an array of integers
    @return: the number of unique integers
    """
    def deduplication(self, nums):
        # write your code here
        left, right = 0, 0
        visited = set()
        while right < len(nums):
            if nums[right] not in visited:
                nums[left] = nums[right]
                visited.add(nums[right])
                left += 1
            right += 1
        return left
```
