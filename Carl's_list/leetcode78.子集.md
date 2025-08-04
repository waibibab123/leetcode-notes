# 78、子集
题目网址：https://leetcode.cn/problems/subsets/

题目难度：mid

代码语言：cpp
## 题解
回溯

step1.变量设置：
* 记录递归路径上的数组：path
* 记录答案数组：res

step2.递归参数：
* nums：候选元素数组
* index：记录当前递归的是nums的第几个数字

step3.边界条件：每次递归都将path装入res（与排列的不同之处，不是到了叶子结点才装，而是每个结点上的路径都装进去，包括根节点也就是空集）

step4.确定单次遍历逻辑：从index遍历nums，先将元素装入path，再调用递归函数，再恢复现场

C++
```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> path;
    void dfs(vector<int>& nums, int index) {
        res.push_back(path);
        for (int i = index; i < nums.size(); i ++ ) {
            path.push_back(nums[i]);
            dfs(nums, i + 1);
            path.pop_back();
        }
    }
    vector<vector<int>> subsets(vector<int>& nums) {
        dfs(nums, 0);
        return res;
    }
};
```
