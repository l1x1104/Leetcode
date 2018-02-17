[对称数之二](https://leetcode.com/problems/strobogrammatic-number-ii/description/)

- Solution 1: Recursion
```java
class Solution {
    public List<String> findStrobogrammatic(int n) {
        return helper(n, n);
    }

    List<String> helper(int n, int m) {
        if (n == 0) return new ArrayList<String>(Arrays.asList(""));
        if (n == 1) return new ArrayList<String>(Arrays.asList("0", "1", "8"));
    
        List<String> list = helper(n - 2, m);   
        List<String> res = new ArrayList<String>(); 
        System.out.println("n=" + n + ",  list.size=" + list.size());
        for (int i = 0; i < list.size(); i++) {
            String s = list.get(i);     
            if (n != m) res.add("0" + s + "0");
            res.add("1" + s + "1");
            res.add("6" + s + "9");
            res.add("8" + s + "8");
            res.add("9" + s + "6");
        }
        
        return res;
    }
}
```

- Solution 2: Recursive
```java
public class Solution {
    public List<String> findStrobogrammatic(int n) {
        List<String> one = Arrays.asList("0", "1", "8"), two = Arrays.asList(""), res = two;
        if(n % 2 == 1) {
            res = one;
        }
        for(int i = (n % 2) + 2; i <= n; i += 2) {
            List<String> newList = new ArrayList<>();
            for(String str : res){
                if(i != n) {
                    newList.add("0" + str + "0");
                }
                newList.add("1" + str + "1");
                newList.add("6" + str + "9");
                newList.add("8" + str + "8");
                newList.add("9" + str + "6");
            }
            res = newList;
        }
        return res;   
    }
}
```
