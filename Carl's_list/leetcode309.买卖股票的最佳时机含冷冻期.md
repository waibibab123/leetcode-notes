# 309、买卖股票的最佳时机含冷冻期
题目网址：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/

题目难度：mid

代码语言：cpp

前置题目：[leetcode188、买卖股票的最佳时机4](leetcode188.买卖股票的最佳时机4.md)
## 题解
状态表示需要调整为
```cpp
//dp[i][0]：第i天持有股票的状态
//dp[i][1]: 第i天卖出
//dp[i][2]: 处于冷冻期
//dp[i][3]: 没持有股票，且不处于冷冻期
```
C++
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<int>> dp(n, vector<int>(4, 0));
        dp[0][0] = -prices[0];
        for (int i = 1; i < n; i ++ ) {
            dp[i][0] = max({dp[i - 1][0], dp[i - 1][3] - prices[i], dp[i - 1][2] - prices[i]});
            dp[i][1] = dp[i - 1][0] + prices[i];
            dp[i][2] = dp[i - 1][1];
            dp[i][3] = max(dp[i - 1][3], dp[i - 1][2]);
        }
        return max({dp[n - 1][1], dp[n - 1][2], dp[n - 1][3]});
    }
};
```
