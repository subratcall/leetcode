因为是有顺序的，所以不能用hashmap来保存有的字母。

检查target中的每个字母是不是都能被找到。

```
class Solution:
    """
    @param s: string S
    @param t: string T
    @return: whether S can convert to T
    """
    def canConvert(self, s, t):
        # Write your code here
        if not s:
            return False
        if not t:
            return True
            
        p_t, p_s = 0, 0
        while p_s < len(s) and p_t < len(t):
            if t[p_t] == s[p_s]:
                p_s += 1
                p_t += 1
            else:
                p_s += 1

        return p_t == len(t)

```
