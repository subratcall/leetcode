求和 => 背包

从nums里取数，使得选的这些数之和最接近sum/2
```py
class Solution:
    """
    @param nums: the given array
    @return: the minimum difference between their sums 
    """
    def find_min(self, nums: List[int]) -> int:
        # write your code here
        total = sum(nums)
        m, n = int(total / 2), len(nums)
        # dp[i][j] 前i个数能不能装满容量为j的包
        dp = [[False] * (m + 1) for _ in range(n + 1)]
        dp[0][0] = True
        for i in range(1, n + 1):
            dp[i][0] = True
            for j in range(1, m + 1):
                if nums[i-1] > j:
                    dp[i][j] = dp[i-1][j]
                else:
                    dp[i][j] = dp[i-1][j] or dp[i-1][j - nums[i-1]]
        
        for i in range(m, -1, -1):
            if dp[-1][i]:
                return abs(total - 2 * i)
```
