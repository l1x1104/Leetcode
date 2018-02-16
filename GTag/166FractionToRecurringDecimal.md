[分数转循环小数](https://leetcode.com/problems/fraction-to-recurring-decimal/description/)

```java
public class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        if (numerator == 0) {
            return "0";
        }
        StringBuilder res = new StringBuilder();
        // "+" or "-"
        res.append(((numerator > 0) ^ (denominator > 0)) ? "-" : "");
        long num = Math.abs((long)numerator);
        long den = Math.abs((long)denominator);
        
        // integral part
        res.append(num / den);
        num %= den;
        if (num == 0) {
            return res.toString();
        }
        
        // fractional part
        res.append(".");
        HashMap<Long, Integer> map = new HashMap<Long, Integer>();
        map.put(num, res.length());
        while (num != 0) {
            num *= 10;
            res.append(num / den);
            num %= den;
            if (map.containsKey(num)) {
                int index = map.get(num);
                res.insert(index, "(");
                res.append(")");
                break;
            }
            else {
                map.put(num, res.length());
            }
        }
        return res.toString();
    }
}
```

```java
class Solution {
    public String fractionToDecimal(int numerator, int denominator) {
        int sign1 = numerator > 0 ? 1 : -1, sign2 = denominator > 0 ? 1 : -1;
        long num  = Math.abs((long)numerator);
        long den = Math.abs((long)denominator);
        long out = num / den;
        long remain = num % den;
        String result = Long.toString(out);
        if (sign1 * sign2 == -1 && (out > 0 || remain > 0)) {
            result = "-" + result;
        }
        if (remain == 0) {
            return result;
        }
        
        result += ".";
        int pos = 0;
        Map<Long, Integer> map = new HashMap<>();
        StringBuilder sb = new StringBuilder();
        while (remain != 0) {
            if (map.containsKey(remain)) {
                sb.insert(map.get(remain), "(");
                sb.append(")");
                break;
            }
            map.put(remain, pos);
            sb.append((remain * 10) / den);
            remain = (remain * 10) % den;
            pos++;
        }

        return result + sb.toString();
    }
}
```
