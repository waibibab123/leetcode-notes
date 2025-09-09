# 122、买卖股票的最佳时机2
题目网址：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-ii/submissions/661177027/

题目难度：mid

代码语言：cpp

前置题目：[买卖股票的最佳时机](leetcode121、买卖股票的最佳时机.md)
## 题解
这道题目与121的唯一区别是，可以多次买卖股票，但是同一个时间最多只能持有一股，因此dp[i][0]的递推式会略微发生改变

C++
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        vector<vector<int>> dp(prices.size(), vector<int>(2, 0));
        dp[0][0] = -prices[0];
        for (int i = 1; i < prices.size(); i ++ ) {
            dp[i][0] = max(dp[i - 1][0], dp[i - 1][1] - prices[i]);
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
        }
        return dp[prices.size() - 1][1];
    }
};
```
