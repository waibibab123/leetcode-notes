# 718、最长重复子数组
题目网址：https://leetcode.cn/problems/maximum-length-of-repeated-subarray/submissions/664973232/

题目难度：mid

代码语言：cpp
## 题解
状态表示：dp[i][j]表示：以nums[i-1]为末尾元素的子数组和以nums2[j-1]为末尾元素的子数组，两者的最长公共连续子数组的长度

状态转移：
* nums1[i-1]==nums2[j-1]：当两个数组的当前元素相等时，说明当前元素可以接在“以nums1[i-2]和nums2[j-2]为末尾的公共子数组”后面，形成更长的公共子数组，因此：dp[i][j]=dp[i-1][j-1]+1
* nums1[i-1]!=nums2[j-1]：当两个元素不相等时，以这两个元素为末尾的子数组不可能是公共子数组，因此dp[i][j]为0

C++
```cpp
class Solution {
public:
    int findLength(vector<int>& nums1, vector<int>& nums2) {
        int n = nums1.size();
        int m = nums2.size();
        int res = 0;
        vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));
        for (int i = 1; i <= n; i ++ ) {
            for (int j = 1; j <= m; j ++ ) {
                if (nums1[i - 1] == nums2[j - 1]) dp[i][j] = max(dp[i - 1][j - 1] + 1, dp[i][j]);
                res = max(res, dp[i][j]);
            }
        }
        return res;
    }
};
```
