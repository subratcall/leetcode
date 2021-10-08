```
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        idx_a = len(a) - 1 
        idx_b = len(b) - 1
        
        res = []
        carry = 0
        
        while idx_a >= 0 or idx_b >= 0:
            x = int(a[idx_a]) if idx_a >= 0 else 0
            y = int(b[idx_b]) if idx_b >= 0 else 0
            if x + y + carry == 2:
                total = 0
                carry = 1
            elif x + y + carry == 3:
                total = 1
                carry = 1
            else:
                total = x + y + carry
                carry = 0
            
            idx_a -= 1
            idx_b -= 1
            
            res.append(str(total))
            
        if carry > 0:
            res.append(str(carry))
            
        return "".join(res[::-1])
            
```
