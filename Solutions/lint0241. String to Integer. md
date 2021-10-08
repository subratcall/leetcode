对于这种读数类的题，似乎都需要设置num和sign两个变量。初始值设为0和1。
```
class Solution:
    """
    @param target: A string
    @return: An integer
    """
    def stringToInteger(self, target):
        # write your code here
        num = 0
        sign = 1
        if target[0] == "-":
            sign = -1
        
        for ch in target:
            if ch.isnumeric():
                num = num * 10 + ord(ch) - ord("0")

        return num * sign
```
