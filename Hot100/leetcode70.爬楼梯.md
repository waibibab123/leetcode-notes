# 70、爬楼梯
难度：easy

代码语言：cpp

题目网址：https://leetcode.cn/problems/climbing-stairs/

## 解法
### 方法一、动态规划
状态表示：$`d[i]`$表示当台阶为i阶时，爬到楼顶的方法数

状态转移：因为每次可以爬1或2个台阶，所以爬到第i阶楼梯时，可能是从第i-1阶楼梯上来的，也可能是从第i-2阶楼梯上来的，因此$`d[i] = d[i - 1] + d[i - 2]`$

边界设置：对于第1个台阶，只能从第0个台阶爬1个台阶上来，因此$`d[1] = 1`$，而对于第2个台阶，可能是从第0个台阶爬2个台阶上来，也可能是从第0个台阶爬1阶先到第1个台阶，再从第1个台阶爬1阶到第2个台阶，因此$`d[2] = 2`$

## 代码

C++

```cpp
class Solution {
public:
    int climbStairs(int n) {
        if (n == 1) return 1;
        if (n == 2) return 2;
        vector<int> dp(n + 1, 0);
        dp[1] = 1;
        dp[2] = 2;
        for (int i = 3; i <= n; i ++ ) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
};
```
