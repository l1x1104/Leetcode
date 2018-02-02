[Reverse String](https://leetcode.com/problems/reverse-string/description/)
- Solution 1: Iterative Swapping Using Two Pointers
```java
public class Solution {
    public String reverseString(String s) {
        char[] word = s.toCharArray();
        int i = 0;
        int j = s.length() - 1;
        while (i < j) {
            char temp = word[i];
            word[i] = word[j];
            word[j] = temp;
            i++;
            j--;
        }
        return new String(word);
    }
}
```
* Space is needed to transform string to byte array <br>
- Solution 2: 
```java
public class Solution {
    public String reverseString(String s) {
        byte[] bytes = s.getBytes();
        int i = 0;
        int j = s.length() - 1;
        while (i < j) {
            byte temp = bytes[i];
            bytes[i] = bytes[j];
            bytes[j] = temp;
            i++;
            j--;
        }
        return new String(bytes);
    }
}
```
- Solution 3: <br>
Note that this assume that the input string is encoded using ASCII format. This will not work with Unicode value where one character may be more than 1 byte. <br>
```java
public class Solution {
    public String reverseString(String s) {
        char[] word = s.toCharArray();
        int i = 0;
        int j = s.length() - 1;
        while (i < j) {
            word[i] = (char) (word[i] ^ word[j]);
            word[j] = (char) (word[i] ^ word[j]);
            word[i] = (char) (word[i] ^ word[j]);
            i++;
            j--;
        }
        return new String(bytes);
    }
}
```
- Solution 4: Java Library
```java
public class Solution {
    public String reverseString(String s) {
        return new StringBuilder(s).reverse().toString();
    }
}
```
