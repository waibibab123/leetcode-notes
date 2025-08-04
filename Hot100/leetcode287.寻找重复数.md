# 287、寻找重复数
题目难度：mid

题目网址：https://leetcode.cn/problems/find-the-duplicate-number/description/

代码语言：cpp

## 题解
### 方法一、原地哈希
由于数字本身的范围就是在1到n，因此可以把数组本身当成哈希表，具体地，遍历这个数组，假设当前遍历到的元素值为x，就把nums[x]乘以-1，当某次遍历到一个元素y，且nums[y]为负数时，对应的y（与之前的重复）就是重复的元素。

例如：1、3、4、2、2   依次将nums[1] nums[3] nums[4] nums[2]变成负数，当遍历到nums[4]=2时，判断nums[2]为负，因此2为重复元素

但题目中说“不修改nums数组”，因此在得到重复元素后需要把每个数再取绝对值

**代码**
C++

```cpp
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int res = -1;
        for (int i = 0; i < nums.size(); i ++ ) {
            int idx = abs(nums[i]);
            if (nums[idx] < 0) {
                res = idx;
                break;
            }
            nums[idx] *= -1;
        }
        for (int i = 0; i < nums.size(); i ++ ) nums[i] = abs(nums[i]);
        return res;
    }
};
```
