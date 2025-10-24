# 30、串联所有单词的子串
题目难度：hard

代码语言：cpp
## 题解
定长滑动窗口：
* 套路（遍历窗口右侧）：入窗--判断窗口大小--更新结果--出窗
* 本题额外需要：窗口的左侧是存在多个起点；需要跑 wordLen 次起点不同的定长滑动窗口

C++
```cpp
class Solution {
public:
    vector<int> findSubstring(string s, vector<string>& words) {
        int wordsCnt = words.size();
        int wordsLen = words[0].length();
        int windowsLen = wordsCnt * wordsLen;
        vector<int> res;
        unordered_map<string, int> targetFreq;
        for (auto str : words) targetFreq[str] ++ ;
        for (int offset = 0; offset < wordsLen; offset ++ ) {
            int overload = 0;
            unordered_map<string, int> curFreq;
            for (int r = offset + wordsLen; r <= s.length(); r += wordsLen) {
                string curStr = s.substr(r - wordsLen, wordsLen);
                //1.入窗
                if (curFreq[curStr] == targetFreq[curStr]) overload ++ ;
                curFreq[curStr] ++ ;
                //2.判断窗口长度是否达到目标值
                int l = r - windowsLen;
                if (l < 0) continue;
                //3.更新
                if (overload == 0) res.push_back(l);
                //4.出窗
                curStr = s.substr(l, wordsLen);
                curFreq[curStr] -- ;
                if (curFreq[curStr] == targetFreq[curStr]) overload -- ;
            }
        }
        return res;
    }
};
```
