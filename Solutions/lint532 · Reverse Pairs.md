```
class Solution:
    """
    @param A: an array
    @return: total of reverse pairs
    """
    def reversePairs(self, A):
        # write your code here
        if not A:
            return 0
        tmp = [0 for _ in range(len(A))]
        return self.merge_sort(A, tmp, 0, len(A) - 1)

    def merge_sort(self, A, tmp, start, end):
        if start >= end:
            return 0
        mid = start + (end - start) // 2
        #记录逆序对
        sum = 0
        #左区间右区间归并排序
        sum += self.merge_sort(A, tmp, start, mid)
        sum += self.merge_sort(A, tmp, mid + 1, end)

        #合并两个有序数组
        sum += self.merge(A, tmp, start, mid, end)
        return sum

    def merge(self, A, tmp, start, mid, end):
        left_idx, right_idx = start, mid + 1
        idx = start
        sum = 0
        while left_idx <= mid and right_idx <= end:
            if A[left_idx] <= A[right_idx]:
                tmp[idx] = A[left_idx]
                idx += 1
                left_idx += 1
            else:
                tmp[idx] = A[right_idx]
                idx += 1
                right_idx += 1
                #记录reverse pair
                sum += mid - left_idx + 1
            
        while left_idx <= mid:
            tmp[idx] = A[left_idx]
            idx += 1
            left_idx += 1
        while right_idx <= end:
            tmp[idx] = A[right_idx]
            idx += 1
            right_idx += 1

        for i in range(start, end + 1):
            A[i] = tmp[i]

        return sum
```
