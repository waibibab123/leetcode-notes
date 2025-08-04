# 55、跳跃游戏
贪心
维护一个变量ed表示当前能够到达的最远距离，然后从0遍历到ed，遍历过程中，如果检测到ed已经大于等于nums.size()就直接返回true，然后更新ed，如果遍历完还没有返回true，就直接返回false，说明无法到达终点

C++
```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int ed = nums[0];
        for (int i = 0; i <= ed; i ++ ) {
            if (ed >= nums.size() - 1) return true;
            ed = max(ed, i + nums[i]);
        }
        return false;
    }
};
```
