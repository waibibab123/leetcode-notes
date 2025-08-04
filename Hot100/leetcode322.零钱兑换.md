# 322、零钱兑换
难度：mid

代码语言：cpp

题目网址：https://leetcode.cn/problems/coin-change/description/

## 题解
### 方法一、动态规划
**前提知识**：1.熟悉01背包的基本原理 2.熟悉完全背包的基本原理 3.熟悉01背包和完全背包空间优化为O（n）的方法和原理

**类似题目**：本题目与题目leetcode279极为相似

step1.状态表示：我们将$`dp[i]`$表示为凑成总金额i所需的最少的硬币个数

step2.状态转移：我们将这个问题看成是背包容量为n、能恰好装下的物品个数（一个物品可以使用多遍，因此为完全背包），物品集合即是不同面额硬币的集合

因此，我们采用背包问题的遍历方式，第一层循环是对各物品的遍历：`for (int i = 0; i < coins.size(); i ++ )` ，第二层循环是对背包容量开始遍历，因为是完全背包，因此采用的是正向遍历`for (int j = coins[i]; j <= amount; j ++ )`，
对于$`dp[j]`$来说，是分为两种情况的，第一种情况是选择硬币i，此时`dp[j] = dp[j - coins[i]] + 1`，第二种情况是不选择硬币i，此时$`dp[j]`$保持不变，两种情况取最小值即可。

step3、边界处理：当背包容量为0时，凑成总金额所需的最少硬币个数为0

## 代码
C++

```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        vector<int> dp(amount + 1, 0x3f3f3f3f);
        dp[0] = 0;
        for (int i = 0; i < coins.size(); i ++ ) {
            for (int j = coins[i]; j <= amount; j ++ ) {
                dp[j] = min(dp[j], dp[j - coins[i]] + 1);
            }
        }
        return dp[amount] == 0x3f3f3f3f ? -1 : dp[amount];
    }
};
```
