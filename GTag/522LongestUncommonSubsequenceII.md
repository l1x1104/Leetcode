[最长非共同子序列之二](https://leetcode.com/problems/longest-uncommon-subsequence-ii/description/)

遍历所有字符串，将每一个遍历到的字符串与数组中剩下的字符串依次比对，看某一个字符串子是不是它的子序列，如果都不是的话，那么当前字符串就是一个非共同子序列，用其长度来更新结果res

- Solution 1: 暴力解
```java
class Solution {
    public int findLUSlength(String[] strs) {
        int res = -1, j = 0, n = strs.length;
        for (int i = 0; i < n; i++) {
            for (j = 0; j < n; j++) {
                if (i == j) continue;
                if (checkSub(strs[i], strs[j])) {
                    break;
                }
            }
            if (j == n) {
                res = Math.max(res, strs[i].length());
            }
        }
        
        return res;
    }
    private boolean checkSub(String sub, String s) {
        int idx = 0;
        char[] ch = s.toCharArray();
        for (char c: ch) {
            if (c == sub.charAt(idx)) idx++;
            if (idx == sub.length()) break;
        }
        return idx == sub.length();
    }
}
```

- Solution 2: Sort + checkSubsequence
```java
    public int findLUSlength(String[] strs) {
        Arrays.sort(strs, new Comparator<String>() {
            public int compare(String o1, String o2) {
                return o2.length() - o1.length();
            }
        });
        
        Set<String> duplicates = getDuplicates(strs);
        for(int i = 0; i < strs.length; i++) {
            if(!duplicates.contains(strs[i])) {
                if(i == 0) return strs[0].length();
                for(int j = 0; j < i; j++) {
                    if(isSubsequence(strs[j], strs[i])) break;
                    if(j == i-1) return strs[i].length();
                }
            }
        }
        return -1;
    }
    
    public boolean isSubsequence(String a, String b) {
        int i = 0, j = 0;
        while(i < a.length() && j < b.length()) {
            if(a.charAt(i) == b.charAt(j)) j++;
            i++;
        }
        return j == b.length();
    }
    
    private Set<String> getDuplicates(String[] strs) {
        Set<String> set = new HashSet<String>();
        Set<String> duplicates = new HashSet<String>();
        for(String s : strs) {
            if(set.contains(s)) duplicates.add(s);
            set.add(s);
        }
        return duplicates;
    }
```
