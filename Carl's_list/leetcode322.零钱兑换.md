# 322、零钱兑换
题目网址：https://leetcode.cn/problems/coin-change/description/

题目难度：mid

代码语言：cpp

前置题目：[leetcode518、零钱兑换](leetcode518.零钱兑换2.md)
## 题解
与518基本一致，唯一不同的是这里不是求组合数，而是求最小值，此时递推过程变为：
```cpp
int a = dp[j - coins[i]] + 1;//选coins[i]
int b = dp[j];//不选coins[i]
dp[j] = min(a, b);
```

C++
```cpp
class Solution {
public:
    int coinChange(vector<int>& coins, int amount) {
        int n = coins.size();
        vector<int> dp(amount + 1, 0x3f3f3f3f);
        dp[0] = 0;
        for (int i = 0; i < n; i ++ ) {
            for (int j = coins[i]; j <= amount; j ++ ) {
                dp[j] = min(dp[j], dp[j - coins[i]] + 1);
            }
        }
        return dp[amount] == 0x3f3f3f3f ? -1 : dp[amount];
    }
};
```
