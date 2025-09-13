# 188、买卖股票的最佳时机
题目网址：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/submissions/662222582/

题目难度：mid

代码语言：cpp

前置题目：[leetcode123、买卖股票的最佳时机](leetcode123.买卖股票的最佳时机3.md)
## 题解
这道题相对于123更加一般化，最多可以买卖k个股票，我们就把dp的第二个维度设置成k*2

C++
```cpp
class Solution {
public:
    int maxProfit(int k, vector<int>& prices) {
        int n = prices.size();
        int res = 0;
        vector<vector<int>> dp(n, vector<int>(k * 2, 0));
        for (int i = 0; i < k * 2; i += 2) {
            dp[0][i] = -prices[0];
        }
        for (int i = 1; i < n; i ++ ) {
            for (int j = 0; j < k * 2; j += 2) {
                dp[i][j] = (j != 0) ? max(dp[i - 1][j], dp[i - 1][j - 1] - prices[i]) : max(dp[i - 1][j], - prices[i]);
                dp[i][j + 1] = max(dp[i - 1][j + 1], dp[i - 1][j] + prices[i]);
                if (i == n - 1) res = max(dp[i][j + 1], res);
            }
        }
        return res;
    }
};
```
