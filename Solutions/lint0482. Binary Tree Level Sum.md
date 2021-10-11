## 解法1： BFS
从资源利用的角度，BFS要比DFS好，因为DFS为了得到答案，必须遍历整棵树。而BFS走到需要的那一层就可以停止。
```
class Solution:
    """
    @param root: the root of the binary tree
    @param level: the depth of the target level
    @return: An integer
    """
    def levelSum(self, root, level):
        # write your code here
        if not root:
            return 0
        que = collections.deque([root])
        count = 0
        res = 0
        flag = False
        while que and not flag:
            count += 1
            if count == level:
                flag = True
            n = len(que)
            for _ in range(n):
                node = que.popleft()
                if flag:
                    res += node.val
                if node.left:
                    que.append(node.left)
                if node.right:
                    que.append(node.right)
                
        return res
```

## 解法2: DFS
代码略短一些
```
class Solution:
    """
    @param root: the root of the binary tree
    @param level: the depth of the target level
    @return: An integer
    """
    def levelSum(self, root, level):
        # write your code here
        def dfs(root, level, target_level):
            if not root:
                return
            if level == target_level:
                self.res += root.val
            dfs(root.left, level + 1, target_level)
            dfs(root.right, level + 1, target_level)
            
        self.res = 0
        dfs(root, 1, level)
        return self.res
```
