# leetcode121、买卖股票的最佳时机
题目网址：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/

题目难度：mid

代码语言：cpp
## 题解
动态规划

状态表示：
* dp[i][0]：第i天为“买入态”时的最大利润
* dp[i][1]：第i天为“卖出态”时的最大利润

这里“买入态”指的是截止到第i天（包含第i天）已经买入了股票，因此包含了两种情况，第一种情况是第i天买的，此时dp[i][0] = -prices[i]，第二种情况是第i天之前买的，此时dp[i][0] = dp[i - 1][0]

这里“卖出态”指的是截止到第i天（包含第i天）已经卖出了股票，也包含两种情况，第一种是第i天卖出的，此时dp[i][1] = dp[i - 1][0] + prices[i]，第二种情况是第i天之前卖出的，此时dp[i][1] = dp[i - 1][1]

C++
```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        vector<vector<int>> dp(prices.size(), vector<int>(2, 0));
        dp[0][0] = -prices[0];
        for (int i = 1; i < prices.size(); i ++ ) {
            dp[i][0] = max(dp[i - 1][0], - prices[i]);
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
        }
        return dp[prices.size() - 1][1];
    }
};
```
