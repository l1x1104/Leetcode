[计算各位不相同的数字个数](https://leetcode.com/problems/count-numbers-with-unique-digits/description/)

DFS
```JAVA
public class Solution {
	public int countNumbersWithUniqueDigits(int n) {
		if (n > 10) {
			return countNumbersWithUniqueDigits(10);
		}else if(n == 1) {
			return 10;
		}else if(n == 0) {
			return 1;
		}
		boolean[] used = new boolean[10];
		List<Integer> tempList = new ArrayList<>();
		helper(n, used, tempList);
		return res + 10;
	}
	

	public int res = 0;
	
	public void helper(int n, boolean[] used, List<Integer> tempList) {
		if(tempList.size() == n) {
			res++;
			return ;
		}	
		for(int i = 0 ; i < 10; i++) {
			if(used[i] || (tempList.size() == 0 && i == 0)) {
				continue;
			}
			used[i] = true;
			tempList.add(i);
			helper(n, used, tempList);
			tempList.remove(tempList.size() - 1);
			used[i] = false;
		}		
		return ;
	}
}
```
