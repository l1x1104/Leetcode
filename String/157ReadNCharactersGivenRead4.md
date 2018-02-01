[Read N Characters Given Read4](https://leetcode.com/problems/read-n-characters-given-read4/description/)

```java
public class Solution extends Reader4 {
    /**
     * @param buf Destination buffer
     * @param n   Maximum number of characters to read
     * @return    The number of characters read
     */
    public int read(char[] buf, int n) {
        
        char[] buffer = new char[4];
        boolean endOfFile = false;
        int readBytes = 0;
        
        while (readBytes < n && !endOfFile) {
            int currReadBytes = read4(buffer);
            if (currReadBytes !=4) {
                endOfFile = true;
            }
            int length = Math.min(n - readBytes, currReadBytes);
            for (int i = 0; i < length; i++) {
                buf[readBytes + i] = buffer[i];
            }
            readBytes += length;
        }
        
        return readBytes;
    }
}
```
