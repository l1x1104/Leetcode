***
#### Given two strings, the task is to check whether these strings are meta strings or not. Meta strings are the strings which can be made equal by exactly one swap in any of the strings. Equal string are not considered here as Meta strings.

* Examples: <br>
  Input : str1 = "geeks" <br>
  &#8194; &#8194; &#8194;&#8194;str2 = "keegs" <br>
  Output : Yes <br>
  By just swapping 'k' and 'g' in any of string, both will become same.
  
 * Examples: <br>
  Input : str1 = "rsting" <br>
  &#8194; &#8194; &#8194;&#8194;str2 = "string  <br>
  Output : No
  
##### Algorithm
- Check if both strings are of equal length or not, if not return false.
- Start comparing, count number of unmatched characters and also store the index of unmatched characters.
- If unmatched characters are more than 2 then return false.
- Check if on swapping any of these two characters in any string would make the string equal or not.
- If yes then return true. Otherwise return false.

```java
private boolean areMetaString(String str1, String str2) {
    if (str1.length() != str2.length()) return false; 
    
    int prev = -1, curr = -1, count = 0;
    for (int i = 0; i < str1.length(); i++) {
        if (str1.charAt(i) != str2.charAt(i)) {
            count ++;
            if (count > 2) {
                return false;
            }
            prev = curr;
            prev = i;
        }
    }
    return (count == 2 && str1.charAt(prev) == str2.charAt(curr) && str2.charAt(prev) == str1.charAt(curr));
}
```
#### FOLLOW UP 两个string，求问能否通过n次swap互相转换，假设swap之间不重合。(str[0] <->str[2] 以后 str[2]和str[0]就不会和其他位置swap)
##### Algorithm
- 用hash table + two pointer。对于每个index，如果char一样就跳过，不match就把"str2->str1" 存到hash table里，表示有candidate swap，下一次看  到不match的char，就看"str1->str2" 在不在hash里
<br> </br>
方法就是构建一个String, 存到HashTable里面. 代码类似下面:
···java
  ...
  String str = p[0] + "a" + p[1];
  set.add(str);
  ...
  for(int[] p:points){
        String str = (sum-p[0]) + "a" + p[1];
        if( !set.contains(str))
            return false;
        
   }
```

