# 349、两个数组的交集
题目网址：https://leetcode.cn/problems/intersection-of-two-arrays/description/

题目难度：mid

代码语言：cpp
## 题解
注意一下vector转unordered_set的方法就可以了

C++

```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> set1(nums1.begin(), nums1.end());
        unordered_set<int> set2(nums2.begin(), nums2.end());
        vector<int> res;
        for (auto item : set1) {
            if (set2.contains(item)) res.push_back(item);
        }
        return res;
    }
};
```
