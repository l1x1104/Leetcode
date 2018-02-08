[最短完整的单词](https://leetcode.com/problems/shortest-completing-word/description/)

```java
class Solution {
    public String shortestCompletingWord(String licensePlate, String[] words) {
        int[] count = new int[26];
        char[] ch1 = licensePlate.toLowerCase().toCharArray();
        
        for (int i = 0; i < ch1.length; i++) {
            if (Character.isLetter(ch1[i])) {
                count[ch1[i] - 'a']++;
            }
        }
        
        int len = Integer.MAX_VALUE; 
        String result = null;
        for (String word: words) {
            System.out.println(word);
            char[] ch = word.toCharArray();
            int[] countWord = new int[26];
            for (int i = 0; i < ch.length; i++) {
                countWord[ch[i] - 'a']++;
            }           
            if (isComplete(countWord, count)) {
                if (ch.length < len) {
                    len = ch.length;
                    result = word;
                }
            }
            
        }
        
        return result;
    }
    private boolean isComplete(int[] countWord, int[] count) {
        for (int i = 0; i < 26; i++) {
            if (countWord[i] < count[i]) {
                return false;
            }
        }
        return true;
    }
}
```
