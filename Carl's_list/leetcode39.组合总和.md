# 39、组合总和
题目网址：https://leetcode.cn/problems/combination-sum/description/

题目难度：mid

代码语言：cpp
## 题解
回溯

step1.变量设置：
* 记录递归路径上的数组：path
* 记录答案数组：res

step2.递归参数：
* candidates：候选元素数组
* index：记录当前递归的是candidates的第几个数字
* target：path数组中所有元素的和与目标和的差值

step3.边界条件：当target == 0说明到达了递归树的叶子结点

step4.确定单次遍历逻辑：遍历candidates，对于每次遍历，保证此时target > 0 首先将此元素加入path，target减去此元素值，然后调用递归函数，最后恢复现场（target加上此元素值&元素从path中pop）

C++
```cpp
class Solution {
public:
    vector<vector<int>> res;
    vector<int> path;
    void dfs(vector<int>& candidates, int target, int startIndex) {
        if (target == 0) {
            res.push_back(path);
            return;
        }
        for (int i = startIndex; i < candidates.size() && target > 0; i ++ ) {
            path.push_back(candidates[i]);
            target -= candidates[i];
            dfs(candidates, target, i);
            target += candidates[i];
            path.pop_back();
        }
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        dfs(candidates, target, 0);
        return res;
    }
};
```
