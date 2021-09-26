一些不成熟的总结：

这题没有像其他题目一样，先一次性求出所有prefix。原因之一可能是为了提高效率。别的题是要求所有可能的情况，所以必须要遍历一遍。

但是这题只要求符合条件的答案。可能在前面几个数字就已经得到答案了，所以没必要先把所有prefix_sum都求出来。

另外这题有两个要求：start和end都要尽可能地小。end尽可能小实际不难，因为只要我们是从左向右遍历就好。

start尽可能小，则需要我们在记录visted的时候，只保存第一次出现的时候的index。这样就解决了。
```
class Solution:
    """
    @param arr: The array 
    @param k: the sum 
    @return: The length of the array
    """
    def searchSubarray(self, arr, k):
        # Write your code here
        #前缀和->前缀
        d = dict()
        d[0] = -1
        prefix_sum = 0
        for i in range(len(arr)):
            prefix_sum += arr[i]
            if (prefix_sum - k) in d:
                return i - d[prefix_sum - k]
            # 只保留起始位置最小的。如果已经有了，就不更新
            if prefix_sum not in d:
                d[prefix_sum] = i
            
        return -1

```
