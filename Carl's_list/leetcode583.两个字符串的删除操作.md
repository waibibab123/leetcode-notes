# 583、两个字符串的删除操作
题目网址：https://leetcode.cn/problems/delete-operation-for-two-strings/description/

题目难度：mid

代码语言：cpp
## 题解
dp[i][j]表示将word1的前i个字符转换为word2的前j个字符所需的最少删除次数

若word1[i-1] == word2[j-1]（当前字符相同）：
dp[i][j] = dp[i-1][j-1]（无需任何操作）
若当前字符不同：
dp[i][j] = min(删除word1对应的字符, 删除word2对应的字符，都删除) = min(dp[i - 1][j] + 1, dp[i][j - 1] + 1, dp[i - 1][j - 1] + 2]

C++
```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        int n = word1.size();
        int m = word2.size();
        vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0x3f3f3f3f));
        for (int i = 0; i <= n; i ++ ) dp[i][0] = i;
        for (int i = 0; i <= m; i ++ ) dp[0][i] = i;
        for (int i = 1; i <= n; i ++ ) {
            for (int j = 1; j <= m; j ++ ) {
                if (word1[i - 1] == word2[j - 1]) dp[i][j] = dp[i - 1][j - 1];
                else dp[i][j] = min({dp[i - 1][j - 1] + 2, dp[i - 1][j] + 1, dp[i][j - 1] + 1});
            }
        }
        return dp[n][m];
    }
};
```
