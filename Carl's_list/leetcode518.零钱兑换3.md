# 518、零钱兑换3
题目网址：https://leetcode.cn/problems/coin-change-ii/description/

题目难度：mid

代码语言：cpp
## 题解
完全背包的变形

复习：完全背包递推式的推导：
```cpp
f[i , j ] = max( f[i-1,j] , f[i-1,j-v]+w ,  f[i-1,j-2*v]+2*w , f[i-1,j-3*v]+3*w , .....)
f[i , j-v]= max(            f[i-1,j-v]   ,  f[i-1,j-2*v] + w , f[i-1,j-3*v]+2*w , .....)
由上两式，可得出如下递推关系： 
                        f[i][j]=max(f[i,j-v]+w , f[i-1][j]) 
```

C++
```cpp
class Solution {
public:
    int change(int amount, vector<int>& coins) {
        vector<int>dp(amount + 1, 0);
        dp[0] = 1;
        for (int i = 0; i < coins.size(); i ++ ) {
            for (int j = coins[i]; j <= amount; j ++ ) {
                dp[j] += (long long)dp[j - coins[i]];
            }
        }
        return dp[amount];
    }
};
```
