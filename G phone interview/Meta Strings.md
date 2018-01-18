#### Given two strings, the task is to check whether these strings are meta strings or not. Meta strings are the strings which can be made equal by exactly one swap in any of the strings. Equal string are not considered here as Meta strings.

* Examples: <br>
  Input : str1 = "geeks" <br>
          str2 = "keegs" <br>
  Output : Yes <br>
  By just swapping 'k' and 'g' in any of string, both will become same.
  
* Examples: <br>
  Input : str1 = "rsting" <br>
          str2 = "string  <br>
  Output : No
  
##### Algorithm:
- Check if both strings are of equal length or not, if not return false.
- start comparing, count number of unmatched characters and also store the index of unmatched characters.
- If unmatched characters are more than 2 then return false.
- check if on swapping any of these two characters in any string would make the string equal or not.
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
