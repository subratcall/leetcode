本题可以拆分成两个子问题：
1. 数字相加减求结果（运算符不存在优先级，依次从左到右运算即可）；
2. 运算符有优先级，乘除的优先级高于加减；

第一个问题比较简单，容易解决。

需要特别注意的是，sign赋值的那里，有多种可能。能走到那一步的，一定是读取完数字后，i+1的位置。换言之，是数字后面一位。所以，有可能是运算符，还有可能是空格。

因此，判断sign=="?"这步，要进行if, elif处理，即只处理+-，忽略是空格的情况。而不能用else。

- *这里写码有个小感受。在遍历的时候，如果说每个元素的操作有的多有的少、有复杂的操作、需要对指针的走动有比较强的控制时，用while循环就更方便一些。而for循环更适合单纯的遍历。while循环的缺点是要注意边界控制，下标访问不能出界。*
```
class Solution:
    def calculate(self, s: str) -> int:
        i, num = 0, 0
        sign = "+"
        stack = []
        
        while i < len(s):
            # deal with spaces
            if s[i].isspace():
                i += 1
                continue
            # deal with numbers
            while i < len(s) and s[i].isdigit():
                num = num * 10 + int(s[i])
                i += 1
            
            if sign == "+":
                curr = num
                stack.append(curr)
            elif sign == "-":
                curr = -num
                stack.append(curr)

            # 这里要注意，实际是有三种情况
            if i < len(s):
                sign = s[i]
            
            # reset the number
            num = 0
            i += 1
            
        return sum(stack)
```


对于第二个子问题，只需要对前面的operator部分进行修改。弹出num_1，进行操作后把结果压栈。
```
class Solution:
    def calculate(self, s: str) -> int:
        i, num = 0, 0
        sign = "+"
        stack = []
        
        while i < len(s):
            # deal with spaces
            if s[i].isspace():
                i += 1
                continue
            # deal with numbers
            while i < len(s) and s[i].isdigit():
                num = num * 10 + int(s[i])
                i += 1
            
            if sign in "+-":
                curr = num if sign == "+" else -num
                stack.append(curr)
            if sign in "*/":
                curr = stack.pop() * num if sign == "*" else int(stack.pop() / num)
                stack.append(curr)

            if i < len(s):
                sign = s[i]
            
            # reset the number
            num = 0
            i += 1
            
        return sum(stack)
```
