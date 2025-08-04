# 139、单词拆分
难度：mid

代码语言：cpp

题目网址：https://leetcode.cn/problems/word-break/

## 题解
### 方法一、动态规划
**思路来源**：《代码随想录》

step1.状态表示：我们把$`dp[i]`$表示为字符串s的前i个字符能否被wordDict拼出来，如果值为true则可以被拼出来，值为false则不能被拼出来

step2.状态转移：我们在第一层循环对字符串s进行遍历，假设遍历到第i个字符，第二层循环对子串字典wordDict进行遍历，假设遍历到子串字典第j个子串wordDict[j]。

如何进行状态转移？如果确定dp[x]为true，且[x, y]这个区间的子字符串出现在字典中，那么dp[i]一定是true，所以递推公式是，如果[x, y]这个区间的子字符串出现在字典中，同时dp[x]为true，那么dp[y]为true

step3.边界处理：如果字符串s是一个空串，那么它一定可以被子串字典中的子串拼接表示（即一个子串都不选），因此dp[0] = true

## 代码
C++

```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        vector<bool> dp(s.length() + 1, false);
        dp[0] = true;
        for (int j = 1; j <= s.length(); j ++ ) {
            for (int i = 0; i < wordDict.size(); i ++ ) {
                if (j >= wordDict[i].size()) {
                    string temp = s.substr(j - wordDict[i].size(), wordDict[i].size());
                    dp[j] = dp[j] || (dp[j - wordDict[i].size()] && wordDict[i] == temp);
                }
            }
        }
        return dp[s.length()];
    }
};
```
