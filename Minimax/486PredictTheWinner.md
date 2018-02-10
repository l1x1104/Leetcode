[Predict the Winner](https://leetcode.com/problems/predict-the-winner/description/)

- Solution 1: BS
```java
public class Solution extends GuessGame {
    public int guessNumber(int n) {
        int l = 1, r = n, num = 0;
        
        while(l <= r) {
            int mid = l + (r - l) / 2;
            if(guess(mid) == 1) {
                l = mid + 1;
            }else if(guess(mid) == -1) {
                r = mid;
            }else if(guess(mid) == 0) {
                return mid;
            }
        }
        return 0;
    }
}
```
