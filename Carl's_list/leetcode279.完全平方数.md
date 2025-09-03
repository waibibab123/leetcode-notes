# 279、完全平方数
题目网址：https://leetcode.cn/problems/perfect-squares/submissions/659141248/

题目难度：mid

代码语言：cpp

前置题目：[leetcode518、零钱兑换](leetcode518.零钱兑换2.md)
## 题解
和518基本一样，唯一不同的是这里变成了求最小值，以及没有具体的物品，而是变成了各个平方数的值

C++
```cpp
class Solution {
public:
    int numSquares(int n) {
        vector<int> dp(n + 1, 0x3f3f3f3f);
        dp[0] = 0;
        for (int i = 1; i <= n / i; i ++ ) {
            for (int j = i * i; j <= n; j ++ ) dp[j] = min(dp[j], dp[j - i * i] + 1);
        }
        return dp[n];
    }
};
```
