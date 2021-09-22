## 解法1: Recursion
容易写
```
class Solution:
    """
    @param root: the root of the binary tree
    @return: An integer
    """
    def leafSum(self, root):
        # write your code here
        if not root:
            return 0
        if not root.left and not root.right:
            return root.val
        return self.leafSum(root.left) + self.leafSum(root.right)
```

## 解法2: Traverse
```
class Solution:
    """
    @param root: the root of the binary tree
    @return: An integer
    """
    def leafSum(self, root):
        # write your code here
        self.leaf = 0
        self.traverse(root)
        return self.leaf

    def traverse(self, root):
        if not root:
            return
        if not root.left and not root.right:
            self.leaf += root.val
        
        self.traverse(root.left)
        self.traverse(root.right)
```
