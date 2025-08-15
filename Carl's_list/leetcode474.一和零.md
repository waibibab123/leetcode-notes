# 474、一和零
题目网址：https://leetcode.cn/problems/ones-and-zeroes/description/

题目难度：mid

代码语言：cpp
## 题解
动态规划

依旧是01背包的变形，不同的地方有：

* 1.每个物品的价值为1
* 2.每个物品的体积包含了两个维度需要分别考虑

C++
```cpp
class Solution {
public:
    int findMaxForm(vector<string>& strs, int m, int n) {
        vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
        for (auto str : strs) {
            int zero_cnt = 0;
            int one_cnt = 0;
            for (auto c : str) {
                if (c == '0') zero_cnt ++ ;
                else one_cnt ++ ;
            }
            for (int i = m; i >= zero_cnt; i -- ) {
                for (int j = n; j >= one_cnt; j -- ) {
                    dp[i][j] = max(dp[i][j], dp[i - zero_cnt][j - one_cnt] + 1);
                }
            }
        }
        return dp[m][n];
    }
};
```
