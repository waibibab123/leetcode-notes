# 45、跳跃游戏2
题目网址：https://leetcode.cn/problems/jump-game-ii/?envType=study-plan-v2&envId=top-interview-150

题目难度：mid

代码语言：cpp
## 题解
采用贪心策略：
1. 维护当前能到达的最远位置max_ed
2. 遍历当前可到达范围内的所有位置，计算能跳到的新最远位置
3. 每完成一轮遍历（即跳一步），更新max_ed并增加步数
4. 当max_ed覆盖到终点时，返回当前步数

C++
```cpp
class Solution {
public:
    int jump(vector<int>& nums) {
        int res = 0;
        int n = nums.size();
        if (n == 1) return res;
        int max_ed = 0;
        for (int i = 0; i <= max_ed; i ++ ) {
            int cur_ed = max_ed;
            for (int j = i; j <= cur_ed; j ++ ) {
                max_ed = max(max_ed, j + nums[j]);
            }
            res ++ ;
            if (max_ed >= n) return res;
        }
        return res;
    }
};
```
