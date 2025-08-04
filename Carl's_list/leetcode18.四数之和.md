# 18、四数之和
题目网址：https://leetcode.cn/problems/4sum/description/

题目难度：mid

代码语言：cpp

## 题解
### 方法一、双指针
在leetcode15的基础上，添加一个额外指针，思路完全相同

C++

```cpp
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> res;
        sort(nums.begin(), nums.end());
        for (int i = 0; i < nums.size(); i ++ ) {
            if (i > 0 && nums[i - 1] == nums[i]) continue;
            int j = i + 1;
            for (; j < nums.size(); j ++ ) {
                if (j > i + 1 && nums[j - 1] == nums[j]) continue;
                int l = j + 1, r = nums.size() - 1;
                while (l < r) {
                    if ((long long)nums[i] + nums[j] + nums[l] + nums[r] == target) {
                        res.push_back({nums[i], nums[j], nums[l], nums[r]});
                        while (l < r && nums[l + 1] == nums[l]) l ++ ;
                        while (l < r && nums[r - 1] == nums[r]) r -- ;
                        l ++ ;
                        r -- ;
                    }
                    else if ((long long)nums[i] + nums[j] + nums[l] + nums[r] > target) r -- ;
                    else l ++ ;
                }
            }
        }
        return res;
    }
};
```
