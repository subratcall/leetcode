## 解法1: Hash
TC：O(N) SC:O(N)

用hash的话，不需要输入是有序的。但是会消耗额外空间。

本题数组已经有序，后访问的数肯定比访问过的数要大。只要找num-abs(target)就可以。如果是无序的，得考虑+-target。
```
class Solution:
    def twoSum7(self, nums, target):
        # write your code here
        visited = set()

        if target == 0:
            for num in nums:
                if num in visited:
                    return [num, num]
                visited.add(num)

        for num in nums:
            if num - abs(target) in visited:
                return [num- abs(target), num]
            visited.add(num)
```

## 解法2: 有序数组 + 二分
TC：O(NlogN) SC:O(1)

数据规模很大时，不能用hash表存到内存，那就要考虑别的办法。有没有另外的办法，能快速地确定一个元素在不在集合中呢？

那就是二分法。

```
class Solution:
    def twoSum7(self, nums, target):
        # write your code here
        for i in range(len(nums)):
            j = self.binary_search(nums, i+1, len(nums) - 1, nums[i] + abs(target))
            if j != -1:
                return [nums[i], nums[j]]
        return [-1, -1]

    def binary_search(self, nums, left, right, target):
        while left + 1 < right:
            mid = (left + right) // 2
            if nums[mid] >= target:
                right = mid
            else:
                left = mid
        if nums[left] == target:
            return left
        if nums[right] == target:
            return right

        return -1
```

## 解法3: 同向双指针
TC：O(N) SC:O(1)

对于每个i，找到第一个j，使得nums[j] - nums[i] >= target
```
class Solution:
    """
    @param nums: an array of Integer
    @param target: an integer
    @return: [num1, num2] (num1 < num2)
    """
    def twoSum7(self, nums, target):
        # write your code here
        target = abs(target)
        j = 1
        for i in range(len(nums)):
            j = max(j, i + 1)  # 要保证j始终在i右边 反例：[0,1,2] 0
            while j < len(nums) and nums[j] - nums[i] < target:
                j += 1
            if j == len(nums):
                break
            if nums[j] - nums[i] == target:
                return [nums[i], nums[j]]

        return [-1, -1]
```
