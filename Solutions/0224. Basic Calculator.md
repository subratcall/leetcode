可以先写没有括号版本的
```
class Solution:
    """
    @param s: the given expression
    @return: the result of expression
    """
    def calculate(self, s):
        # Write your code here
        number = 0
        sign = 1
        result = 0
        for ch in s:
            if ch in "1234567890":
                number = number * 10 + int(ch)
            elif ch == "+":
                result += sign * number
                sign = 1
                number = 0
            elif ch == "-":
                result += sign * number
                sign = -1
                number = 0

        result += sign * number
        return result
```

在此基础上，添加对括号的处理。
```
class Solution:
    """
    @param s: the given expression
    @return: the result of expression
    """
    def calculate(self, s):
        # Write your code here
        number = 0
        sign = 1
        result = 0
        stack = []
        for ch in s:
            if ch in "1234567890":
                number = number * 10 + int(ch)
            elif ch == "+":
                result += sign * number
                sign, number = 1, 0
            elif ch == "-":
                result += sign * number
                sign, number = -1, 0
            elif ch == "(":
                stack.append(result)
                stack.append(sign)
                number, sign, result = 0, 1, 0
            elif ch == ")":
                result += sign * number
                prev_sign = stack.pop()
                prev_result = stack.pop()
                result = prev_result + prev_sign * result
                # 这里要注意把number清零。
                number = 0

        result += sign * number
        return result

```
