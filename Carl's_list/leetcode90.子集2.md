# 90、子集2
题目网址：https://leetcode.cn/problems/subsets-ii/description/

题目难度：mid

代码语言：cpp
## 题解
前提知识：[leetcode40题解](leetcode40.组合总和2.md)和 [leetcode78题解](leetcode78.子集.md)

这道题在78的基础上，添加了40的树层去重思想

C++
```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> path;
    unordered_map<int, int> used;
    void dfs(vector<int>& nums, int index, unordered_map<int, int> used) {
        res.push_back(path);
        for (int i = index; i < nums.size(); i ++ ) {
            if (i > 0 && nums[i] == nums[i - 1] && used[nums[i]] == false) continue;
            path.push_back(nums[i]);
            used[nums[i]] = true;
            dfs(nums, i + 1, used);
            path.pop_back();
            used[nums[i]] = false;
        }
    }
    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        dfs(nums, 0, used);
        return res;
    }
};
```
