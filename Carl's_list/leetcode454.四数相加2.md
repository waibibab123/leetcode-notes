# 454、四数相加2
题目网址：https://leetcode.cn/problems/4sum-ii/description/

题目难度：mid

代码语言：cpp

## 题解
### 方法一、哈希
首先记录nums1和nums2的所有和的组合结果到哈希表中，key为相加的值，value为出现的次数，然后遍历nums3和nums4的组合，对于某个和sum，查看哈希表中之前出现过多少次-sum，次数累加到答案中

C++

```cpp
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        int res = 0;
        unordered_map<int, int> mp;
        for (int a = 0; a < nums1.size(); a ++ ) {
            for (int b = 0; b < nums2.size(); b ++ ) {
                mp[nums1[a] + nums2[b]] ++ ;
            }
        }
        for (int c = 0; c < nums3.size(); c ++ ) {
            for (int d = 0; d < nums4.size(); d ++ ) {
                res += mp[-1 * (nums3[c] + nums4[d])];
            }
        }
        return res;
    }
};
```
