# 121.买卖股票的最佳时机

难度：easy

代码语言：cpp

题目网址：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/

## 解法

### 方法一、动态规划

状态表示：$`d[i][j]`$代表第i天的状态为j，其中当j==0时表示买入态，可以是当天买了股票，也可以是之前买了股票但是还没有卖出；当j==1时表示卖出态，同理，可以是当天卖出了股票，也可以是之前卖出。

状态转移：

* 当j==0时，分为两种情况，当天买和之前已经买了，如果是当天买，由于限定只能买入和卖出一支股票，因此$`d[i][0] = -prices[i]`$（初始的利润为0），如果不是当天买的，那么说明前一天一定也是“买入态”，因此$`d[i][0] = d[i - 1][0]`$
* 当j==1时，同理，如果是当天卖出，则$`d[i][1] = prices[i]`$，如果不是当天卖出，则前一天也一定是“卖出态”，因此$`d[i][1] = d[i - 1][1]`$

边界设置：对于第0天，j==0时，说明必然是第0天买了股票，因此$`d[i][0] = -prices[0]`$，j==1时，说明是第0天先买入了股票，然后又卖了，因此$`d[i][1] == 0`$

## 代码

C++

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        vector<vector<int>> dp(prices.size(), vector<int>(2, 0));
        dp[0][0] = -prices[0];
        dp[0][1] = 0;
        for (int i = 1; i < prices.size(); i ++ ) {
            dp[i][0] = max(dp[i - 1][0], -prices[i]);
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
        }
        return dp[prices.size() - 1][1];
    }
};
```
