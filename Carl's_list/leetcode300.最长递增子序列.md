# 300、最长递增子序列
题目网址：https://leetcode.cn/problems/longest-increasing-subsequence/description/

题目难度：mid

代码语言：cpp
## 题解
状态表示：`dp[i]`表示以下标为i的元素结尾的最长递增子序列的长度

状态转移：对于i，当nums[i]前面的一个元素nums[j]（j < i）小于nums[i]时，有`dp[i] = max(dp[i], dp[j] + 1)`

C++
```cpp
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int res = 0;
        int n = nums.size();
        vector<int> dp(n, 1);
        for (int i = 0; i < n; i ++ ) {
            for (int j = 0; j < i; j ++ ) {
                if (nums[j] < nums[i]) dp[i] = max(dp[j] + 1, dp[i]);
            }
            res = max(res, dp[i]);
        }
        return res;
    }
};
```
