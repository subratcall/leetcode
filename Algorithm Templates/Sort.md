# Merge Sort
```
class Solution:
    """
    @param A: an integer array
    @return: nothing
    """
    def sortArray(self, A):
        # write your code here
        if not A:
            return 
        tmp = [0 for _ in range(len(A))]
        self.merge_sort(A, tmp, 0, len(A) - 1)
        return A
    
    def merge_sort(self, A, tmp, start, end):
        if start >= end:
            return
        #取中间位置，把数组分成两半
        mid = start + (end - start) // 2
        # divide, 归并排序左右两边
        self.merge_sort(A, tmp, start, mid)
        self.merge_sort(A, tmp, mid + 1, end)
        #conquer 合并两边
        self.merge(A, tmp, start, mid, end)

    def merge(self, A, tmp, start, mid, end):
        #start->mid, mid+1 -> end
        #分别记录处理到了哪个位置
        left_idx = start
        right_idx = mid + 1

        #在tmp中对应的位置
        idx = start
        #合并两个有序数组
        while left_idx <= mid and right_idx <= end:
            if A[left_idx] <= A[right_idx]:
                #左小于右
                tmp[idx] = A[left_idx]
                idx += 1
                left_idx += 1
            else:
                #右小于左
                tmp[idx] = A[right_idx]
                idx += 1
                right_idx += 1
            
        while left_idx <= mid:
            tmp[idx] = A[left_idx]
            idx += 1
            left_idx += 1
        while right_idx <= end:
            tmp[idx] = A[right_idx]
            idx += 1
            right_idx += 1
        #更新原数组
        for i in range(start, end + 1):
            A[i] = tmp[i]
```

# Quick Sort
```
class Solution:
    """
    @param A: an integer array
    @return: nothing
    """
    def sortIntegers2(self, A):
        # write your code here
        if not A:
            return 

        self.quickSort(A, 0, len(A) - 1)

    def quickSort(self, A, start, end):
        #出口
        if start >= end:
            return 

        #拆解， partition, 双指针， 左边都小于pivot，右边都大于
        left, right = start, end
        #选基准，随机，一般选取中点
        pivot = A[start + (end - start) // 2]
        
	      #退出条件，left > right
        while left <= right:
            #找左边开始，第一个大于等于pivot的位置
            while left <= right and A[left] < pivot:
                left += 1
            #找右边开始，第一个小于等于pivot的位置
            while left <= right and A[right] > pivot:
                right -= 1
            
            if left <= right:
                #左右互换
                A[left], A[right] = A[right], A[left]
                left += 1
                right -= 1
        
        self.quickSort(A, start, right)
        self.quickSort(A, left, end)

```
