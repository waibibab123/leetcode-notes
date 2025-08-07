# 343、整数拆分
题目网址：https://leetcode.cn/problems/integer-break/submissions/650767766/

题目难度：mid

代码语言：cpp
## 题解
动态规划

状态表示：dp[i]表示i拆分整数的最大乘积

我们遍历j从1到i-1，那么dp[i]就由两种可能组成，一种是将i拆分成j和i-j，另一种是将i拆分成j之后，再将i-j继续拆分，这两种情况分别的代码为：`j * (i - j)和j * dp[i - j]`

为什么没有“dp[j] * dp[i - j]”的情况？因为j从1到i-1遍历的过程中，已经包含完了所有的j拆分可能性

C++
```cpp
class Solution {
public:
    int integerBreak(int n) {
        vector<int>dp(n + 1, 0);
        dp[2] = 1;
        for (int i = 3; i <= n; i ++ ) {
            for (int j = 1; j < i; j ++ ) 
            dp[i] = max({dp[i], j * (i - j), j * dp[i - j]});
        }
        return dp[n];
    }
};
```
