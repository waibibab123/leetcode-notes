# 72、编辑距离
题目网址：https://leetcode.cn/problems/edit-distance/description/

题目难度：mid

代码语言：cpp

前置题目：[leetcode583.两个字符串的删除操作](leetcode583、两个字符串的删除操作)
## 题解
与583的区别：
* word1的增加操作可以等价为word2的删除操作，因此二者等价
* 替换操作可以看成两次删除，因此只需把dp[i - 1][j - 1] + 2换成dp[i - 1][j - 1] + 1

C++
```cpp
class Solution {
public:
    int minDistance(string word1, string word2) {
        vector<vector<int>> dp(word1.size() + 1, vector<int>(word2.size() + 1, 0x3f3f3f3f));
        for (int i = 0; i <= word1.size(); i ++ ) dp[i][0] = i;
        for (int i = 0; i <= word2.size(); i ++ ) dp[0][i] = i;
        for (int i = 1; i <= word1.size(); i ++ ) {
            for (int j = 1; j <= word2.size(); j ++ ) {
                if (word1[i - 1] == word2[j - 1]) dp[i][j] = min(dp[i - 1][j - 1], dp[i][j]);
                else {
                    dp[i][j] = min({dp[i - 1][j] + 1, dp[i][j - 1] + 1, dp[i - 1][j - 1] + 1});
                }
            }
        }
        return dp[word1.size()][word2.size()];
    }
};
```
