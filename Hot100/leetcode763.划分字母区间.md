# 763、划分字母区间

难度：mid

代码语言：cpp

题目网址：https://leetcode.cn/problems/partition-labels/

## 解法
### 方法一、贪心

思路：首先找出每一种字母（在字符串中出现过的）的区间范围，然后使用leetcode56.合并区间的方式进行区间合并。

举例：ababcbacadefegdehijhklij

* a的区间范围是：[0, 8]
* b的区间范围是：[1, 5]
* c的区间范围是：[4, 7]
* d的区间范围是：[9, 14]
* e的区间范围是：[10, 15]
* f的区间范围是：[11, 11]
* g的区间范围是：[13, 13]
* h的区间范围是：[16, 19]
* i的区间范围是：[17, 22]
* j的区间范围是：[18, 23]
* k的区间范围是：[20, 20]
* l的区间范围是：[21, 21]

对上述十二个区间进行区间合并后的结果：[[0, 8], [9, 15], [16, 23]]，三个区间的长度分别为：[9, 7, 8]，即最终结果

## 代码

C++

```cpp
class Solution {
public:
    vector<int> partitionLabels(string s) {
        unordered_map<char, pair<int, int>> scale_per_char;
        vector<pair<int, int>> segs;
        vector<pair<int, int>> res;
        //计算各区间
        for (int i = 0; i < s.length(); i ++ ) {
            if (!scale_per_char.count(s[i])) scale_per_char[s[i]] = {i, i};
            else scale_per_char[s[i]].second = i;
        }
        for (auto mp : scale_per_char) segs.push_back({mp.second.first, mp.second.second});
        //合并区间
        sort(segs.begin(), segs.end());
        int st = -2e9, ed = -2e9;
        for (auto seg : segs) {
            if (ed < seg.first) {
                if (st != -2e9) res.push_back({st, ed});
                st = seg.first, ed = seg.second;
            }
            else ed = max(ed, seg.second);
        }
        if (st != -2e9) res.push_back({st, ed});
        //统计结果
        vector<int> lens;
        for (int i = 0; i < res.size(); i ++ ) {
            lens.push_back(res[i].second - res[i].first + 1);
        }
        return lens;
    }
};
```
