[群组错位词](https://leetcode.com/problems/group-anagrams/description/)

class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> result = new ArrayList<>();
        Map<String, List<String>> map = new HashMap<>();
        for (String s: strs) {
            char[] sArr = s.toCharArray();
            Arrays.sort(sArr);
            String hs = String.valueOf(sArr);
            map.putIfAbsent(hs, new ArrayList<String>());
            map.get(hs).add(s);
        }
        for (Map.Entry<String, List<String>> entry: map.entrySet()) {
            result.add(entry.getValue());
        }
        
        return result;
    }
}
