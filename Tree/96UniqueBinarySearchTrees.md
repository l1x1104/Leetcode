***
#### Given n, how many structurally unique BST's (binary search trees) that store values 1...n?
* For example,
- Given n = 3, there are a total of 5 unique BST's.

Great Explanation https://discuss.leetcode.com/topic/8398/dp-solution-in-6-lines-with-explanation-f-i-n-g-i-1-g-n-i <br>

1. G(n) = F(1, n) + F(2, n) + ... + F(n, n). 
2. F(i, n) = G(i-1) * G(n-i)	1 <= i <= n <br>

Combining the above two formulas, we obtain the recursive formula for G(n). i.e. <br>
G(n) = G(0) * G(n-1) + G(1) * G(n-2) + … + G(n-1) * G(0) 

```java
public int numTrees(int n) {
    int [] G = new int[n+1];
    G[0] = G[1] = 1;
    
    for(int i=2; i<=n; ++i) {
    	for(int j=1; j<=i; ++j) {
    		G[i] += G[j-1] * G[i-j];
    	}
    }

    return G[n];
}
```
