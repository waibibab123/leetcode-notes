# 169、多数元素
题目难度：easy

题目网址：https://leetcode.cn/problems/majority-element/solutions/3660936/mo-er-tou-piao-by-hei-an-qi-shi-7m1e/?envType=study-plan-v2&envId=top-100-liked

代码语言：cpp

## 题解
### 方法一、摩尔投票法
这是一个空间复杂度为O（1）的方法，初始的候选数为数组的第一个数，票数为1，如果当前的遍历值与候选值不同，则票数减一，否则票数加一，如果票数为0，那么更改候选值为当前遍历的值，因为如果一个数出现频率超过一半，那么它票数永远不会被减为0
，具体可以看下面代码的注释

**代码**

C++

```cpp
class Solution {
public:
    // 函数用于找出数组中的多数元素
    int majorityElement(std::vector<int>& nums) {
        // x 用于记录当前可能的多数元素，初始化为 0
        int x = 0;
        // votes 用于记录当前元素的票数，初始化为 0
        int votes = 0;
        // 遍历数组中的每个元素
        for (int num : nums) {
            // 如果当前票数为 0，说明之前记录的元素 x 不再是可能的多数元素，将当前元素 num 赋值给 x
            if (votes == 0) {
                x = num;
            }
            // 如果当前元素 num 等于 x，则票数加 1，否则票数减 1
            votes += (num == x) ? 1 : -1;
        }
        // 最终 x 即为多数元素
        return x;
    }
};
```
