# 139、单词拆分
题目网址：https://leetcode.cn/problems/word-break/submissions/660431223/

题目难度：mid

代码语言：cpp

前置题目：
* [leetcode518、零钱兑换](leetcode518.零钱兑换2.md)
* [leetcode377、组合总数4](leetcode377.组合总和4.md)

## 题解
根据两个前置题目，可以把该题目看成一个容量为s.size()的背包，wordDict中的子串为一个一个物品，现在需要判断物品能否**按照顺序**去凑成背包的值，既然是按照顺序，就需要按照377中的“先背包、后物品”的遍历方式，此外每个子串可以使用无限次，因此就是518中的
完全背包的正序遍历形式，综上：

C++
```cpp
class Solution {
public:
    bool wordBreak(string s, vector<string>& wordDict) {
        vector<bool> dp(s.size() + 1, false);
        dp[0] = true;
        for (int j = 1; j <= s.size(); j ++ ) {
            for (int i = 0; i < wordDict.size(); i ++ ) {
                if (j >= wordDict[i].size()) {
                    string temp = s.substr(j - wordDict[i].size(), wordDict[i].size());
                    dp[j] = dp[j] || (dp[j - wordDict[i].size()] && (wordDict[i] == temp));
                }
            }
        }
        return dp[s.size()];
    }
};
```
