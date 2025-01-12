# Check-if-a-Parentheses-String-Can-Be-Valid

A parentheses string is a non-empty string consisting only of '(' and ')'. It is valid if any of the following conditions is true:

It is ().
It can be written as AB (A concatenated with B), where A and B are valid parentheses strings.
It can be written as (A), where A is a valid parentheses string.
You are given a parentheses string s and a string locked, both of length n. locked is a binary string consisting only of '0's and '1's. For each index i of locked,

If locked[i] is '1', you cannot change s[i].
But if locked[i] is '0', you can change s[i] to either '(' or ')'.
Return true if you can make s a valid parentheses string. Otherwise, return false.

class Solution:
    def canBeValid(self, s: str, locked: str) -> bool:
        n=len(s)
        if n&1==1: return False
        
        bMin, bMax=0, 0  # Initialize balance
        
        for i, c in enumerate(s):
            op=c== '('
            wild=locked[i]=='0'
            
            # Update balances
            if (not op) or wild: bMin-=1  
            else: bMin+=1  
            
            if op or wild: bMax+=1  
            else: bMax-=1  
            
            if bMax < 0: return False
            
            bMin = max(bMin, 0)
        
        # Check if the parentheses can be 
        return bMin==0
        
