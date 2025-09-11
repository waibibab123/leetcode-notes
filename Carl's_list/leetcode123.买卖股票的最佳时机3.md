# 123、买卖股票的最佳时机3

题目网址：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iii/submissions/661580890/

题目难度：hard

代码语言：cpp

前置题目：
* [leetcode121、买卖股票的最佳时机](leetcode121.买卖股票的最佳时机.md)
* [leetcode122、买卖股票的最佳时机2](leetcode122.买卖股票的最佳时机2.md)

## 题解
这道题目与122的区别在于，限定了能够买卖的股票数量，因此这里定义四种不同的状态：
```cpp
/*
    dp[i][0]:第i天持有股票（第一笔交易的股票）
    dp[i][1]:第i天没有持有股票（卖出了第一笔交易的股票，但是还没有买第二笔）
    dp[i][2]:第i天持有股票（第一笔的股票已经卖出，现在持有的是第二笔交易的股票）
    dp[i][3]:第i天没有持有股票（卖出了第二笔交易的股票）
*/
```

C++
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        vector<vector<int>> dp(prices.size(), vector<int>(4, 0));
        dp[0][0] = -prices[0];
        dp[0][2] = -prices[0];
        for (int i = 1; i < prices.size(); i ++ ) {
            dp[i][0] = max(dp[i - 1][0], -prices[i]);
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
            dp[i][2] = max(dp[i - 1][2], dp[i - 1][1] - prices[i]);
            dp[i][3] = max(dp[i - 1][3], dp[i - 1][2] + prices[i]);
        }
        return max(dp[prices.size() - 1][1], dp[prices.size() - 1][3]);
    }
};
```
