Given a sequence of bracket characters, determine if you can make it into a  valid sequence with at most one deletion of any character. Return 1 if it is possible to make it into a valid sequence and return 0 if it is not possible.



Definition of a valid sequence:

1. all the parentheses are matched (every opening bracket-like character has a corresponding closing character)

2. the matched parentheses are in the correct order (an opening bracket-like character should come before the closing bracket-like character)

Assume "{[()]}" are the only brackets we will see. 



Examples of a valid sequence:

[ ( ) ]
( [  ] )

Examples of an invalid sequence:

) (

[ }

[ ( ] )

Solution1:

We can use the solution in " leetcode 20: valid parentheses" to check if a string is valid without any deletion. 

Check the input string is valid. If is valid, return 1. If not, we consider one deletion. 

Iterate each possible index to delete, and check if the rest of the string is valid. 

This method has a O(n^2) time complexity.

Solution 2:

The method we use is still similar to leetcode20. But when we find an unmatched character, we have to possible solutions: one is to ignore the character, and the other is to ignore the previous  element. 
And then we check the new strings, to see if one of them can be valid.

def isValid(s, can_delete):
    if not s:
        return True
    stack = []
    mapping = {")": "(", "}": "{", "]": "["}
    

    for idx, ch in enumerate(s):
        if ch in mapping:
            if stack:
                top = stack.pop()
                top_element = top[1]
                top_idx = top[0]
            else:
                if can_delete:
                    s0 = s[idx + 1:]
                    return isValid(s0, False)
                return False
                
                
            if mapping[ch] != top_element:
                if not can_delete:
                    return False
                else:
                    # possible solution 1: ignore current character
                    s1 = s[:idx] + s[idx+1:]
                    # possible solution 2: ignore current top element

                    s2 = s[:top_idx] + s[top_idx+1:]
                    return isValid(s1, False) or isValid(s2, False)
        else:
            stack.append((idx, ch))

    return not stack
