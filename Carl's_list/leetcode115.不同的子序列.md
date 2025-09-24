# 115、不同的子序列
题目网址：https://leetcode.cn/problems/distinct-subsequences/description/

题目难度：mid

代码语言：cpp
## 题解
状态表示：dp[i][j] 表示 s 的前 i 个字符中包含 t 的前 j 个字符的子序列的数量。

状态转移：

* 如果 s[i-1] == t[j-1]（当前字符匹配）：
  * 可以选择使用 s[i-1] 来匹配 t[j-1]，此时数量为 dp[i-1][j-1]
  * 也可以选择不使用 s[i-1]，此时数量为 dp[i-1][j]
  * 总和为两者之和
* 如果字符不匹配：只能选择不使用 s[i-1]，数量为 dp[i-1][j]

C++
```cpp
class Solution {
public:
    int numDistinct(string s, string t) {
        int n = s.length(), m = t.length();
        vector<vector<long long>> dp(n + 1, vector<long long>(m + 1, 0));
        for (int i = 0; i <= n; i ++ ) dp[i][0] = 1;
        for (int i = 1; i <= m; i ++ ) dp[0][i] = 0;
        for (int i = 1; i <= n; i ++ ) {
            for (int j = 1; j <= m; j ++ ) {
                if (s[i - 1] == t[j - 1] && INT_MAX - dp[i - 1][j] > dp[i - 1][j - 1]) 
                    dp[i][j] = (long long)(dp[i - 1][j - 1] + dp[i - 1][j]);
                else 
                    dp[i][j] = dp[i - 1][j];
            }
        }
        return dp[n][m];
    }
};
```
