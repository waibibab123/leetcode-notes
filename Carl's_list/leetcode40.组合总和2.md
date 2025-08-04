# 40、组合总和2
题目网址：https://leetcode.cn/problems/combination-sum-ii/description/

题目难度：mid

代码语言：cpp
## 题解
回溯

step1.变量设置：
* 记录递归路径上的数组：path
* 记录答案数组：res
* 记录去重数组：used

step2.递归参数：
* candidates：候选元素数组
* StartIndex：记录当前递归的是candidates的第几个数字
* target：path数组中所有元素的和与目标和的差值
* used:去重数组

step3.边界条件：当target == 0说明到达了递归树的叶子结点

step4.确定单次遍历逻辑：遍历candidates，对于每次遍历，保证此时target > 0 首先将此元素加入path，target减去此元素值，标记去重数组，然后调用递归函数，最后恢复现场（target加上此元素值&元素从path中pop，恢复去重数组）

去重：每次遍历的时候满足：`i > 0 && candidates[i - 1] == candidate[i] && used[candidates[i]] == false`的时候要跳过此次遍历，举一个例子，候选数组为`[1,1,2,3]`，当选完第一个1之后，这个分支的子树就变成了从`[1,2,3]`中选，如果此时
不选1，那就变成了从`[2,3]`中选，因为刚开始已经选过一个1了，因此这个子分支A上的所有情况就是“在选完1的前提下，从2,3中选”。回到第一层递归，准备选第二个1时，此时满足上述去重条件，直接跳过，因为此分支下包含的情况与子分支A是完全相同的。

C++
```cpp
class Solution {
public:
    vector<int> path;
    vector<vector<int>> res;
    unordered_map<int, int> used;
    void dfs(vector<int>& candidates, int startIndex, int target, unordered_map<int, int> used) {
        if (target == 0) {
            res.push_back(path);
            return;
        }
        for (int i = startIndex; i < candidates.size() && candidates[i] <= target; i ++ ) {
            if (i > 0 && candidates[i - 1] == candidates[i] && used[candidates[i]] == false) continue;
            target -= candidates[i];
            used[candidates[i]] = true;
            path.push_back(candidates[i]);
            dfs(candidates, i + 1, target, used);
            target += candidates[i];
            used[candidates[i]] = false;
            path.pop_back();
        }
    }
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        dfs(candidates, 0, target, used);
        return res;
    }
};```
