本题如果用DFS，排列组合，共有2^n种方案，TC:O(n*2^n)

DP的TC: O(mn)
## dp[i][j]前i个物品，能不能组成和为j
```py
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param a: Given n items with size A[i]
    @return: The maximum size
    """
    def back_pack(self, m: int, A: List[int]) -> int:
        n = len(A)
        # dp[i][j]前i个物品，能不能组成和为j
        dp = [[False] * (m + 1) for _ in range(n + 1)]
        for i in range(n + 1):
            dp[i][0] = True

        for i in range(1, n + 1):
            for j in range(1, m + 1):
                # 放的了，考虑放与不放
                if A[i-1] <= j:
                    dp[i][j] = dp[i-1][j - A[i-1]] or dp[i-1][j]
                # 放不了，只能不放
                else:
                    dp[i][j] = dp[i-1][j]

        for i in range(m, -1, -1):
            if dp[-1][i]:
                return i
```

## dp[i][j]前i个物品，能把容量为j的背包装多满
```py
class Solution:
    """
    @param m: An integer m denotes the size of a backpack
    @param a: Given n items with size A[i]
    @return: The maximum size
    """
    def back_pack(self, m: int, A: List[int]) -> int:
        n = len(A)
        # dp[i][j]前i个物品，能把容量为j的背包装多满
        dp = [[0] * (m + 1) for _ in range(n + 1)]

        for i in range(1, n + 1):
            for j in range(1, m + 1):
                # 放的了，则考虑放或者不放
                if  j - A[i-1] >= 0:
                    dp[i][j] = max(dp[i-1][j - A[i-1]] + A[i-1], dp[i-1][j])
                # 直接放不了，那就只能不放
                else:
                    dp[i][j] = dp[i-1][j]
        return dp[-1][m]
```
这种写法的效率略低于前一种。因为加法运算的速度低于逻辑运算。
