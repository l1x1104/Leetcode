[Valid Palindrome](https://leetcode.com/problems/valid-palindrome/description/) 
```
For example, 
"A man, a plan, a canal: Panama" is a palindrome. 
"race a car" is not a palindrome. 
```
```java
class Solution {
    public boolean isPalindrome(String s) {
        if(s.length() == 0) return true;
        s = s.trim().toLowerCase();  
        int p1 = 0, p2 = s.length()-1; 
        
        while(p1 < p2){
            while(!alphanumeric(s.charAt(p1)) && p1 < s.length() - 1) p1++;
            while(!alphanumeric(s.charAt(p2)) && p2 > 0) p2--;
            if(p1 >= p2) return true; 
            if(s.charAt(p1) == s.charAt(p2)){
                p1++; 
                p2--; 
            }else {
                return false; 
            }
        }
        return true; 
    }
    
    private boolean alphanumeric(char c){
        if( c - '0' >= 0 && c - '0' <= 9 ) return true; 
        if( c - 'a' >= 0 && c - 'z' <= 0 ) return true; 
        return false; 
    }
}
```
