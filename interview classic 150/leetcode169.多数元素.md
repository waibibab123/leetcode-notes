# 169、多数元素
题目网址：https://leetcode.cn/problems/majority-element/description/?envType=study-plan-v2&envId=top-interview-150

题目难度：easy

代码语言：cpp
## 题解
摩尔投票法

初始化当前最多的元素为res，投票数为votes，然后开始遍历数组

对于当前遍历到的元素x，如果votes为0，则可以将res赋值为x，否则：
* 如果x != res，votes -- 减少res作为最终最多元素的票数
* 如果x == res，votes ++ 增加res作为最终最多元素的票数

遍历结束后的res即最终的最多元素

C++
```cpp
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int res = 0;
        int votes = 0;
        for (int i = 0; i < nums.size(); i ++ ) {
            if (votes == 0) res = nums[i];
            if (nums[i] != res) votes -- ;
            else votes ++ ;
        }
        return res;
    }
};
```
