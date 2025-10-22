# 11、盛最多水的容器
题目网址：https://leetcode.cn/problems/container-with-most-water/description/?envType=study-plan-v2&envId=top-interview-150

题目难度：mid

代码语言：cpp
## 题解
双指针，left、right分别指向两侧，对于值小的一侧让其向中间移动直到找到比原来大的值，求一次容量，知道两个指针相遇

C++
```cpp
class Solution {
public:
    int maxArea(vector<int>& height) {
        int left = 0, right = height.size() - 1;
        int res = 0;
        while (left < right) {
            res = max(res, (right - left) * min(height[left], height[right]));
            if (height[left] < height[right]) {
                int temp = height[left];
                while (left < right && height[left] <= temp) left ++ ;
            } else {
                int temp = height[right];
                while (left < right && height[right] <= temp) right -- ;
            }
        }
        return res;
    }
};
```
