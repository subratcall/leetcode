```py
def binarySearch(nums, target):
    if not nums:
        return -1
        
    left, right = 0, len(nums) - 1
    
    # keep doing binary search when the left not close to the right
    while left + 1 < right:
        mid = (left + right) // 2
        if nums[mid] < target:
            left = mid
        elif nums[mid] > target:
            right = mid
        else:
            #move left or right to the mid, based on which half you wanna continue to search
            left/ right = mid
    
    # in the end, the two pointers will sit besides each other
    # need to check the numbers they're pointing to
    # if looking for the left boundary, then check left first
    # if looking for the right boundary, then check right first
    if nums[left] == target:
        return left
    if nums[right] == target:
        return right
    return -1

```
