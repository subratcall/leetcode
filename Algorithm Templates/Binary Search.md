```
def binarySearch(nums, target):
    if not nums:
        return -1
    start, end = 0, len(nums) - 1
    # 终止条件：相邻的时候就停止
    while left + 1 < right:
        mid = (left + right) // 2
        if nums[mid] < target:
            left = mid
        elif nums[mid] > target:
            right = mid
        else:
            #这里需要根据要求，看移动left还是right
            right = mid
    #最后指针停在相邻位置，分别检查哪个是答案
    #如果是找左边界，就先看left。否则就先看right
    if nums[start] == target:
        return start
    if nums[end] == target:
        return end
    return -1

```
