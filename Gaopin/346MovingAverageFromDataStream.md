[Moving Average from Data Stream](https://leetcode.com/problems/moving-average-from-data-stream/description/)

```JAVA
class MovingAverage {
    private int [] sum;
    private int index, size;
    ///private long sum;
    /** Initialize your data structure here. */
    public MovingAverage(int size) {
        this.size = size;
        sum = new int[size + 1];
        index = 1;        
    }
    
    public double next(int val) {
        if(index < size) {
            sum[index] = sum[index - 1] + val;
            int result = sum[index];
            return (double)result/(index ++);
        } else {
            sum[index % (size + 1)] = sum[(index - 1) % (size + 1)] + val;
            int result = sum[index % (size + 1)] - sum[(index - size)%(size + 1)];
            index ++;
            return (double)result/size;
        }
    }
}
```

```
...这个题如果我要做 follow up 的话，我会问，如果这个 window 很大，比如是最近的 1T 的数据的 average，该怎么办？
使用 Queue 的问题是，Queue 都在内存里，如果内存不够就不知道怎么办了。

那么 1T 的数据假设内存放不下的话，是否有什么办法呢？那只能求助于放在硬盘上了，比如放在数据库里。假如说数据不全在内存里，我怎么可以知道最近的 1T 的数据的 average 是多少呢？我需要去 load 最近的 1T 的数据么？答案是我们记录在硬盘上的值，可以用 PrefixSum 的形式。就是前缀和。那么当你需要计算某一段的和的时候，只需要用当前的前缀和前去之前某个时刻的前缀和就可以了。这样对于硬盘来说，只是读写 1 次。
```
