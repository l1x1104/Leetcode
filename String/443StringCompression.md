[String Compression](https://leetcode.com/problems/string-compression/description/)

```java
class Solution {
    public int compress(char[] chars) {
        int count = 0, index = 0;
        while(index < chars.length){
            char prev = chars[index];
            int number = 0;
            
            while(index < chars.length && chars[index] == prev){
                index++;
                number++;
            }
            chars[count++] = prev;
            if(number != 1)
                for(char c : Integer.toString(number).toCharArray()) 
                    chars[count++] = c;
        }
        return count;
    }
}
```
