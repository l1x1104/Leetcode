[求H指数](https://leetcode.com/problems/h-index/description/)

- Solution 1：Simple sort algo (正)
```java
class Solution {
    public int hIndex(int[] citations) {
        int n = citations.length;
        if (citations == null || n == 0) return 0;
        
        Arrays.sort(citations);
        
        for (int i = 0; i < citations.length; i++) {
            if (n <= citations[i])
                return n;
            else
                n --;
        }
        return n;
    }
}
```
(反) <br>
根据Wiki定义： <br>
First we order the values of f from the largest to the lowest value. Then, we look for the last position in which f is greater than or equal to the position (we call h this position). 
```java
class Solution {
    public int hIndex(int[] citations) {
        int n = citations.length;
        
        Arrays.sort(citations);
        
        int l = 0, r = n - 1;
        for (; l < r; l++, r--) {
            int tmp = citations[r];
            citations[r] = citations[l];
            citations[l] = tmp;
        }
        
        for (int i = 0; i < n; i++) {
            if (i >= citations[i]) {
                return i;
            }
        }
        
        return n;
    }
}
```

- Solution 2: Bucket sort algo
```java
class Solution {
    public int hIndex(int[] citations) {
        int n = citations.length;
        int[] count = new int[n + 1];
       
        for (int i = 0; i < n; i++) {
            if (citations[i] >= n) {
                count[n] ++;
            } else {
                count[citations[i]] ++;
            }
        }
        
        int number = 0;
        for (int j = count.length - 1; j >= 0; j--) {
            number += count[j];
            if (number >= j) {
                return j;
            }
        }
          
        return 0;
    }
}
```
