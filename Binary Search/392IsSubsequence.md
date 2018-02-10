[是子序列](https://leetcode.com/problems/is-subsequence/description/)

- Solution 1: Linear Two Pointers <br>
Time: O(l)(l is length of T)
```java
public class Solution {
    public boolean isSubsequence(String s, String t) {
        if (s.length() == 0) return true;
        int indexS = 0, indexT = 0;
        while (indexT < t.length()) {
            if (t.charAt(indexT) == s.charAt(indexS)) {
                indexS++;
                if (indexS == s.length()) return true;
            }
            indexT++;
        }
        return false;
    }
}
```
```
Follow-Up: t(very huge) only got processed once possible?
If there are lots of incoming S, say S1, S2, ... , Sk where k >= 1B, and you want to check one by one to see if T has its 
subsequence. In this scenario, how would you change your code?
```
```
原理： The prev variable is an index where previous character was picked from the sequence. And for the next character to be 
      picked, you have to select it only after this index is the string ‘T’.
      For instance, if S = "abcd" and T = "abdced".
      The index list mapping looks like,
      a -> 0
      b -> 1
      c -> 3
      d -> 2,5
      e -> 4
      After you pick a, and b, c will be picked, and index is 3. Now if you have to pick d, you can’t pick index 2 because c 
      was picked at 3, so you have to binary search for index which comes after 3. So it returns 5.
```
```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        if (s.length() == 0) return true;
        Map<Character, List<Integer>> map = new HashMap<>();
        
        for (int i = 0; i < t.length(); i++) {
            char ch = t.charAt(i);
            if (!map.containsKey(ch)) {
                List<Integer> tmp = new ArrayList<>();
                tmp.add(i);
                map.put(ch, tmp);
            } else {
                map.get(ch).add(i);
            }
        }
        int lastIndex = -1;
        for (int i = 0; i < s.length(); i++) {
            char ch = s.charAt(i);
            if (!map.containsKey(ch)) return false;
            else {
                List<Integer> tmpList = map.get(ch);
                //int index = Collections.binarySearch(tmpList, lastIndex + 1);
                //if (index < 0) index = -index - 1;
                //if (index == tmpList.size()) return false;
                //lastIndex = tmpList.get(index); 
                int index = binarySearch(tmpList, lastIndex + 1);
                if (index == -1) return false;
                lastIndex = tmpList.get(index);
            }
        }
        return true;
    }
    public int binarySearch (List<Integer> lst, int target) {
        int i = 0, j = lst.size() - 1;
        while (i + 1 < j) {
            int mid = (i + j) / 2;
            if (lst.get(mid) == target) {
                return mid;
            } else if (lst.get(mid) < target) {
                i = mid + 1;
            } else {
                j = mid;
            }
        }
        if (lst.get(i) >= target) return i;
        else if (lst.get(j) >= target) return j;
        return -1;
    }
}
```
