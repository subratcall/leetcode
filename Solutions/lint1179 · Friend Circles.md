

```
class Solution:
    """
    @param M: a matrix
    @return: the total number of friend circles among all the students
    """
    def findCircleNum(self, M):
        # Write your code here
        n = len(M)
        res = 0
        visited = collections.defaultdict(bool)

        for i in range(n):
            #如果已经访问过，则跳过
            if visited[i]:
                continue

            # 如果没有访问过，则另成一派
            res += 1
            visited[i] = True
            # 遍历他的朋友圈
            queue = collections.deque([i])
            visited[i] = True
            while queue:
                person = queue.popleft()
                for j in range(n):
                    # 如果是朋友且没访问过
                    if M[person][j] and not visited[j]:
                        queue.append(j)
                        visited[j] = True
        return res

```
