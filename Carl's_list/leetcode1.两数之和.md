# 1、两数之和
题目网址：https://leetcode.cn/problems/two-sum/submissions/631262283/

题目难度：easy

代码语言：cpp
## 题解
### 方法一、哈希
C++

```cpp
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> mp;
        for (int i = 0; i < nums.size(); i ++ ) {
            if (mp.count(target - nums[i])) {
                return vector<int>{i, mp[target - nums[i]]};
            }
            mp[nums[i]] = i;
        }
        return vector<int>{0, 0};
    }
};
```
