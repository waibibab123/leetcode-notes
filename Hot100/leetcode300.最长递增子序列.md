# 300、最长递增子序列
难度：mid

代码语言：cpp

题目网址：https://leetcode.cn/problems/longest-increasing-subsequence/

## 题解
### 方法一、动态规划

step1.状态表示：我们把dp[i]表示为以下标为i的元素结尾的序列的最长递增子序列

step2.状态转移：我们在第一层循环遍历nums数组，当遍历到下标为i的元素时，进行第二层循环，在第二层循环中遍历所有下标小于i的元素，假设某一个时刻，我们遍历到了下标为j的元素，如果`nums[j] < nums[i]`，
那么就可以考虑在以下标为i的元素结尾的序列的最长递增子序列中加入以下标为j的元素结尾的序列的最长递增子序列，即`dp[i] = max(dp[i], dp[j] + 1)`

step3.边界处理：在第一层循环，我们遍历到下标为i的元素时，要初始化`dp[i] = 1`，也就是说以任何元素结尾的序列的最长递增子序列的长度至少为1（该元素本身组成的子序列）

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
