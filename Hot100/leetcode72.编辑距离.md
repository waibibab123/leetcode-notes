# 72、编辑距离
题目难度：mid

题目网址：https://leetcode.cn/problems/edit-distance/description/

代码语言：cpp

## 题解
### 方法一、动态规划
思路来源：《代码随想录》

step1.状态表示：dp[i][j]表示以下标i-1为结尾的字符串word1和以下标j-1为结尾的字符串word2的最近编辑距离

step2.状态转移：

* 如果word1[i-1] == word2[j-1]，则不执行任何操作，那么dp[i][j] = dp[i-1][j-1]
* 如果word1[i-1] != word2[j-1]，则有增加、删除、替换三种操作:
  * 操作一、word1删除一个元素，那么就是以下标i-2为结尾的word1与以下标j-1为结尾的word2的最近编辑距离再加上一个操作，即dp[i][j]=dp[i-1][j]+1
  * 操作二、word2删除一个元素，那么就是以下标i-1为结尾的word1与以下标j-2为结尾的word2的最近编辑距离再加上一个操作，即dp[i][j]=dp[i][j-1]+1
  * 操作三、把word1[i-1]替换成与word1[j-1]相同的字符，那么就是以下标i-2为结尾的word1与下标j-2为结尾的word2的最近编辑距离再加上一个（替换）操作，即dp[i][j]=dp[i-1][j-1]+1
其中操作二word2删除元素与word1增加元素等价，因此这三个操作包含了所有情况

step3.边界处理：当word1和word2其中一个为空串时，那么最近编辑距离一定为另一个字符串的长度len（即对其中一个空串做len次增加操作，或者对另一个字符串做len次删除操作）

**代码**

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
