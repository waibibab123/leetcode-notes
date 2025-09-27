# 516、最长回文子序列
题目网址：https://leetcode.cn/problems/longest-palindromic-subsequence/

题目难度：mid

代码语言：cpp
## 题解
定义dp[i][j]表示字符串从第 i 个到第 j 个字符之间的最长回文子序列长度

初始化：单个字符的最长回文子序列就是它自己，所以dp[i][i] = 1

从字符串尾部往前遍历（i 从 n 到 1）：

对于每个 i，再从 i+1 往后遍历（j 从 i+1 到 n）

* 如果两端字符相等（s [i-1] == s [j-1]）：那么dp[i][j] = dp[i+1][j-1] + 2（加上这两个相等的字符）
*如果两端字符不等：就取去掉左边字符或去掉右边字符后的最大值（max(dp[i+1][j], dp[i][j-1]）

C++
```cpp
class Solution {
public:
    int longestPalindromeSubseq(string s) {
        int n = s.length();
        vector<vector<int>> dp(n + 1, vector<int>(n + 1, 0));
        for (int i = 1; i <= n; i ++ ) dp[i][i] = 1;
        for (int i = n; i >= 1; i -- ) {
            for (int j = i + 1; j <= n; j ++ ) {
                if (s[i - 1] == s[j - 1]) dp[i][j] = dp[i + 1][j - 1] + 2;
                else dp[i][j] = max(dp[i + 1][j], dp[i][j - 1]);
            }
        }
        return dp[1][n];
    }
};
```
