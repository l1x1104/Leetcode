[求最大子数组乘积](https://leetcode.com/problems/maximum-product-subarray/description/)

```
1. In an array with positive, negative and zero floats, find continuous subarray that has maximum product, output the start and end index of this subarray.
2. Design a data structure storing intervals that supports add an interval and search if a single value is covered by any interval - for example, if the data structure stores [1,2], [3,5], Search(2.5) is false, Search(4.5) is true.
```

```java
public int maxProduct(int[] a) {
  if (a == null || a.length == 0)
    return 0;

  int ans = a[0], min = ans, max = ans;
  
  for (int i = 1; i < a.length; i++) {
    if (a[i] >= 0) {
      max = Math.max(a[i], max * a[i]);
      min = Math.min(a[i], min * a[i]);
    } else {
      int tmp = max;
      max = Math.max(a[i], min * a[i]);
      min = Math.min(a[i], tmp * a[i]);
    }
    
    ans = Math.max(ans, max);
  }
  
  return ans;
}
```
