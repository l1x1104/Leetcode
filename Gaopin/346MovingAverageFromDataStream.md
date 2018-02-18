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
        }else{
            sum[index % (size + 1)] = sum[(index - 1) % (size + 1)] + val;
            int result = sum[index % (size + 1)] - sum[(index - size)%(size + 1)];
            index ++;
            return (double)result/size;
        }
    }
}
```
