# 46、全排列
回溯+去重

C++
```cpp
class Solution {
public:
    vector<int> path;
    vector<vector<int>> res;
    unordered_set<int> used;
    void dfs(vector<int> nums, unordered_set<int> used) {
        if (path.size() == nums.size()) {
            res.push_back(path);
            return;
        }
        for (int i = 0; i < nums.size(); i ++ ) {
            if (used.contains(nums[i])) continue;
            used.insert(nums[i]);
            path.push_back(nums[i]);
            dfs(nums, used);
            path.pop_back();
            used.erase(nums[i]);
        }
    }
    vector<vector<int>> permute(vector<int>& nums) {
        dfs(nums, used);
        return res;
    }
};
```
