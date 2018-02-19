[Substring Anagrams](https://leetcode.com/problems/find-all-anagrams-in-a-string/description/)

- Solution 1: Time O(nl) n is characters in String s, and l is lenth of String p
```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> result = new ArrayList<>();
        if (s.length() < p.length()) {
            return result;
        }
        
        int[] cnt = new int[26], cntP = new int[26];
        for (int i = 0; i < p.length(); i++) {
            cnt[s.charAt(i) - 'a']++;
            cntP[p.charAt(i) - 'a']++;
        }
        
        if (equals(cnt, cntP)) {
            result.add(0);
        }
        
        for (int i = p.length(); i < s.length(); i++) {
            cnt[s.charAt(i) - 'a']++;
            cnt[s.charAt(i - p.length()) - 'a']--;
            if (equals(cnt, cntP)) {
                result.add(i - p.length() + 1);
            }
        }
        
        return result;
    }
    private boolean equals(int[] a, int[] b) {
        for (int idx = 0; idx < a.length; idx++) {
            if (a[idx] != b[idx]) {
                return false;
            }
        }
        return true;
    }
}
```

- Solution 2: O(n)
```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> result = new ArrayList<>();
        if (s.length() < p.length()) {
            return result;
        }
        
        char[] sc = s.toCharArray();
        char[] sp = p.toCharArray();
        
        int[] cnt = new int[256];
        
        for (int i = 0; i < p.length(); i++) {
            cnt[sp[i]]--;
            cnt[sc[i]]++;
        }
        
        int absSum = 0;
        for (int item: cnt) {
            absSum += Math.abs(item);
        }
        if (absSum == 0) {
            result.add(0);
        }
        
        for (int i = p.length(); i < s.length(); i++) {
            absSum = absSum - Math.abs(cnt[sc[i]]) - Math.abs(cnt[sc[i - p.length()]]);
            
            cnt[sc[i]]++;
            cnt[sc[i - p.length()]]--;
            
            absSum = absSum + Math.abs(cnt[sc[i]]) + Math.abs(cnt[sc[i - p.length()]]);
            if (absSum == 0) {
                result.add(i - p.length() + 1);
            }
        }
        
        return result;
    }
}
```
