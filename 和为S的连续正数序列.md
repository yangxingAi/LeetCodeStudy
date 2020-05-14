# 和为S的连续正数序列

## 题目描述：

> 输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。
>
> 序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

## 题目思路：

- 定义一个左边界，一个右边界，左闭右开，形成一个滑动窗口。
- 当窗口内的数值和小于目标值的时候，右边界向前滑动一位，左边界不动，扩大此窗口和。
- 当窗口内的数值小于目标值的时候，左边界向前滑动一位，右边界不动，缩小此窗口和。
- 当等于目标值的时候，记录此窗口内的数值。然后左边界向前滑动一位，继续判断。
- 当左边界的值大于目标值的一半的时候退出循环，因为左边界值大于目标值一半，那么右边界必然大于目标值一半，那么和必然大于目标值，不成立。

## 代码实现:

```java
class Solution {
    public int[][] findContinuousSequence(int target) {
        int i = 1;
        int j =1;
        int sum =0;
        List<int[]> res= new ArrayList<>();
        while(i <= target/2){
            if( sum < target){
                sum += j;
                j++;
            }else if(sum > target){
                sum -= i;
                i++;
            }else{
                int[] arr = new int[j-i];
                for(int k =i ;k < j; k++){
                    arr[k-i] = k;
                }
                res.add(arr);
                sum -= i;
                i++;
            }
        }
        return res.toArray(new int[res.size()][]);
    }
}
```

