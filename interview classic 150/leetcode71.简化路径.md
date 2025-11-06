# 71、简化路径
题目难度：mid

代码语言：cpp
## 题解
参考我的解法：

1.将字符串进行分隔，并去掉多余斜杠

2.利用栈对特殊的.和..进行处理

3.用栈进行字符串组合

C++
```cpp
class Solution {
public:
    string simplifyPath(string path) {
        vector<string> dirs;
        for (int i = 0;  i < path.size(); i ++ ) {
            while (i + 1 < path.size() && path[i + 1] == '/') i ++ ;
            if (i == path.size() - 1) break;
            int j = i + 1;
            while (j < path.size() && path[j] != '/') j ++ ;
            dirs.push_back(path.substr(i + 1, j - i - 1));
            cout << dirs.back() << endl;
            i = j - 1;
        }
        stack<string> st;
        string res;
        for (int i = 0; i < dirs.size(); i ++ ) {
            if (dirs[i] == "." || (dirs[i] == ".." && st.empty())) continue;
            else if (dirs[i] == ".." && !st.empty()) st.pop();
            else st.push(dirs[i]);
        }
        while (!st.empty()) {
            string str = st.top();
            st.pop();
            res = "/" + str + res;
        }
        return res == "" ? "/" : res;
    }
};
```
