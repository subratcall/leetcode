## Divide and Conquer + Memo
```py
class Solution:
    """
    @param grid: a chessboard included 0 and 1
    @return: the shortest path
    """
    def shortest_path2(self, grid: List[List[bool]]) -> int:
        # write your code here
        m, n = len(grid), len(grid[0])
        res = self.cal_shortest_path(grid, m-1, n-1, {})
        return res if res != float("inf") else -1

    def cal_shortest_path(self, grid, i, j, memo):
      m, n = len(grid), len(grid[0])
      if i == 0 and j == 0:
        return 0
      if j < 0 or i < 0 or i >= m or grid[i][j] == 1:
        return float("inf")
      if (i, j) in memo:
        return memo[(i, j)]

      res = float("inf")
      WAYS = [(-1, -2), (-2, -1), (1, -2), (2, -1)]
      for (x, y) in WAYS:
        option = self.cal_shortest_path(grid, i+x, j+y, memo)
        res = min(res, option)
      res = res + 1
      memo[(i, j)] = res

      return res
```

## Top down DP
```py
class Solution:
    """
    @param grid: a chessboard included 0 and 1
    @return: the shortest path
    """
    def shortest_path2(self, grid: List[List[bool]]) -> int:
        # write your code here
        WAYS = [(-1, -2), (-2, -1), (1, -2), (2, -1)]
        m, n = len(grid), len(grid[0])
        dp = [[float('inf')] * n for i in range(m)]
        dp[0][0] = 0
        for j in range(n):
          for i in range(m):
            if grid[i][j] == 1:
              continue
            for delta_x, delta_y in WAYS:
              x, y = i + delta_x, j + delta_y
              if 0 <= x < m and 0 <= y < n:
                dp[i][j] = min(dp[i][j], dp[x][y] + 1)

        return dp[-1][-1] if dp[-1][-1] != float('inf') else -1
```
