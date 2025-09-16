# 714、买卖股票的最佳时机含手续费
题目网址：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/description/

题目难度：mid

代码语言：cpp

前置题目：[leetcode121、买卖股票的最佳时机](leetcode121.买卖股票的最佳时机.md)
## 题解
状态表示
```cpp
/*
    dp[i][0]:第i天持有的股票
    dp[i][1]:第i天卖出股票
    dp[i][2]:第i天没有持有股票，但不是第i天卖出的
*/
```
C++
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int n = prices.size();
        vector<vector<int>> dp(n, vector<int>(3, 0));
        dp[0][0] = -prices[0];
        dp[0][1] = -fee;
        dp[0][2] = 0;
        for (int i = 1; i < n; i ++ ) {
            dp[i][0] = max({dp[i - 1][0], dp[i - 1][1] - prices[i], dp[i - 1][2] - prices[i]});
            dp[i][1] = dp[i - 1][0] + prices[i] - fee;
            dp[i][2] = max(dp[i - 1][2], dp[i - 1][1]);
        }
        return max(dp[n - 1][1], dp[n - 1][2]);
    }
};
```
