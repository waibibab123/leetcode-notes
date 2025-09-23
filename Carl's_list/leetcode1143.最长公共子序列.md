# 1143、最长公共子序列
题目网址：https://leetcode.cn/problems/longest-common-subsequence/description/

题目难度：mid

代码语言：cpp

前置题目：[leetcode718、最长公共子序列](leetcode718.最长重复子数组)
## 题解
与718不同的是，子序列不需要像子数组那样是连续的，因此即使text1[i-1] != text2[j-1]也无需将dp[i][j]置零，此时最长公共子序列有两种可能来源：
* text1[0..i-2]和text2[0..j-1]的最长公共子序列（即跳过text1[i-1]）
* text1[0..i-1]和text2[0..j-2]的最长公共子序列（即跳过text2[j-1]）

直接取两者最大值：dp[i][j] = max(dp[i-1][j], dp[i][j-1])

C++
```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int n = text1.length();
        int m = text2.length();
        vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));
        for (int i = 1; i <= n; i ++ ) {
            for (int j = 1; j <= m; j ++ ) {
                if (text1[i - 1] == text2[j - 1]) dp[i][j] = dp[i - 1][j - 1] + 1;
                dp[i][j] = max({dp[i - 1][j], dp[i][j - 1], dp[i][j]});
            }
        }
        return dp[n][m];
    }
};
```
