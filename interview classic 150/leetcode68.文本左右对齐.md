# 68、文本左右对齐
题目网址：https://leetcode.cn/problems/text-justification/?envType=study-plan-v2&envId=top-interview-150

题目难度：hard

代码语言：cpp
## 题解
贪心，参考自己写的代码

C++
```cpp
class Solution {
public:
    vector<string> fullJustify(vector<string>& words, int maxWidth) {
        vector<string> res;
        for (int i = 0; i < words.size();) {
            int surplus = maxWidth;
            vector<string> temp_words;//记录当前行的所有单词
            vector<int> temp_space;//记录当前行所有空格的长短
            string res_str;
            surplus -= words[i].length();
            temp_words.push_back(words[i]);
            i ++ ;
            //依次判断是否可以放下
            while (i < words.size() && surplus >= (words[i].length() + 1)) {
                temp_words.push_back(words[i]);
                surplus -= (words[i].length() + 1);
                i ++ ;
            }
            //构造每一行的答案串
            if (temp_words.size() == 1) {
                res_str = temp_words[0];
                for (int i = 0; i < surplus; i ++ ) res_str += " ";
            }
            else {
                //计算空格分布
                int interval = temp_words.size() - 1;
                //最后一行（左对齐）
                if (i == words.size()) {
                    for (int j = 0; j < interval; j ++ ) temp_space.push_back(1);
                    temp_space.push_back(surplus);
                    for (int j = 0; j < temp_words.size(); j ++ ) {
                        res_str += temp_words[j];
                        for (int k = 0; k < temp_space[j]; k ++ ) res_str += " ";
                    }
                } else { 
                    //非最后一行（两端对齐）
                    int addition1 = surplus / interval;
                    int addition2 = surplus % interval;
                    for (int j = 0; j < interval; j ++ ) {
                        if (j < addition2) temp_space.push_back(2 + addition1);
                        else temp_space.push_back(1 + addition1);
                    }
                    for (int j = 0; j < temp_words.size(); j ++ ) {
                        res_str += temp_words[j];
                        if (j == temp_words.size() - 1) break;
                        for (int k = 0; k < temp_space[j]; k ++ ) res_str += " ";
                    }
                }
            }
            res.push_back(res_str);
        }
        return res;
    }
};
```
