# 1143、最长公共子序列
题目难度：mid

题目网址：https://leetcode.cn/problems/longest-common-subsequence/description/

代码语言：cpp

## 题解
### 方法一、动态规划
step1.状态表示：`dp[i][j]`表示text1的前i个字符与text2的前j个字符的最长公共子序列

step2.状态转移：

* 若`text1[i - 1] == text2[j - 1]` ， 则 `dp[i][j] = dp[i - 1][j - 1] + 1`
* 否则， `dp[i][j] = max({dp[i - 1][j], dp[i][j - 1], dp[i][j]})`

step3.边界处理：刚开始将dp数组全部初始化为0即可

**代码**

C++ 

```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        int len1 = text1.length();
        int len2 = text2.length();
        vector<vector<int>> dp(len1 + 1, vector<int>(len2 + 1, 0));
        for (int i = 1; i <= len1; i ++ ) {
            for (int j = 1; j <= len2; j ++ ) {
                if (text1[i - 1] == text2[j - 1]) dp[i][j] = dp[i - 1][j - 1] + 1;
                else {
                    dp[i][j] = max({dp[i - 1][j], dp[i][j - 1], dp[i][j]});
                }
            }
        }
        return dp[len1][len2];
    }
};
```
