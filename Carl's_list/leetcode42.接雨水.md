# 42、接雨水
题目网址：https://leetcode.cn/problems/trapping-rain-water/description/

题目难度：hard

代码语言：cpp
## 题解（双指针）
先算出柱子总面积land，即height数组求和的结果，那么接下来如果能算出总面积sum，答案就可以由sum - land得到。因此我们接下来探究如果得到总面积。

我们使用“逐层计算”的策略，刚开始设置双指针left和right分别指向左右边界，初始化当前水位高度为0

在每次循环中，首先找到左右两侧第一个高于当前水位的柱子，计算这两根柱子之间的总面积`(min(height[left],height[right]) - cur) * (right - left + 1)`

随后更新当前水位为新的最小值`min(height[left],height[right])`，然后继续寻找下一层的面积（注意这里的下一层，并不是单纯的加一，而是和cur每次更新有关）

C++

```cpp
class Solution {
public:
    int trap(vector<int>& height) {
        int res = 0;
        int land = 0;
        for (int i = 0; i < height.size(); i ++ ) land += height[i];
        int left = 0, right = height.size() - 1;
        int cur = 0;
        while (left <= right) {
            while (left <= right && height[left] <= cur) left ++ ;
            while (left <= right && height[right] <= cur) right -- ;
            if (left <= right) {
                res += (min(height[left], height[right]) - cur) * (right - left + 1);
                cur = min(height[left], height[right]);
            }
        }
        return res - land;
    }
};
```
