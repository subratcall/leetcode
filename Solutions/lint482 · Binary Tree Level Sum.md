## 解法1： BFS

```
"""
Definition of TreeNode:
class TreeNode:
    def __init__(self, val):
        self.val = val
        self.left, self.right = None, None
"""

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
