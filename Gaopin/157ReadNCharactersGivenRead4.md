[Read N Characters Given Read4](https://leetcode.com/problems/read-n-characters-given-read4/description/)

```java
public class Solution extends Reader4 {
    char[] buffer = new char[4];
    int bufferPtr = 0, bufferCnt = 0;
    
    public int read(char[] buf, int n) {
        int cnt = 0;
        
        while (cnt < n) {
            if (bufferPtr == bufferCnt) {
                bufferCnt = read4(buffer);
                bufferPtr = 0;
            }
            
            if (bufferCnt == 0) {
                break;
            }
            
            while (cnt < n && bufferPtr < bufferCnt) {
                buf[cnt++] = buffer[bufferPtr++];
            }          
        }
        
        return cnt;
    }
}
```
