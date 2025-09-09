# leetcode121、买卖股票的最佳时机
题目网址：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/

题目难度：mid

代码语言：cpp
## 题解
动态规划

状态表示：
* dp[i][0]：第i天为“持有股票”时的最大利润
* dp[i][1]：第i天为“不持有股票”时的最大利润

第i天持有股票包含了两种情况，第一种情况是第i天当天买的股票，此时dp[i][0] = -prices[i]，第二种情况是第i天之前买的，此时dp[i][0] = dp[i - 1][0]

第i天不持有股票，也包含两种情况，第一种是第i天卖出了，此时dp[i][1] = dp[i - 1][0] + prices[i]，第二种情况是第i天没卖出，而是之前压根没买过，此时dp[i][1] = dp[i - 1][1]

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
