[UTF-8 Validation](https://leetcode.com/problems/utf-8-validation/description/)

```java
public class Solution {
    public boolean validUtf8(int[] data) {
		int varCharLeft = 0;
		for (int b: data) {
			if (varCharLeft == 0) {
				if ((b & 0b010000000) == 0)  varCharLeft = 0;
				else if ((b >> 5) == 0b110)  varCharLeft = 1;
				else if ((b >> 4) == 0b1110)  varCharLeft = 2;
				else if ((b >> 3) == 0b11110)  varCharLeft = 3;
				else return false;
			} else {
				if ((b >> 6) != 0b10)  return false;
				varCharLeft--;
			}
		}
		return varCharLeft == 0;
    }
}
```
