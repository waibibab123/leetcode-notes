# 55.跳跃游戏

难度：mid

代码语言：cpp

题目网址：https://leetcode.cn/problems/jump-game/description/

## 解法

### 方法一、贪心

如果数组的长度为1，必然能到达终点，直接返回true即可。

如果数组的长度大于1，维护一个变量ed（初始化为0，表示仅能到达下标为0的元素）表示当前能到达的最远距离，遍历数组下标0到ed的元素，当下标为i时，更新$`ed = max(i + nums[i], ed)`$，随后直接判断当前的ed是否大于等于$`nums.size() - 1`$，
如果是，直接返回true。若直接循环结束还没有返回true，说明无法到达终点。

## 代码
C++

```cpp
class Solution {
public:
    bool canJump(vector<int>& nums) {
        if (nums.size() == 1) return true;
        int ed = nums[0];
        for (int i = 0; i <= ed; i ++ ) {
            ed = max(ed, i + nums[i]);
            if (ed >= nums.size() - 1) return true;
        }
        return false;
    }
};
```
