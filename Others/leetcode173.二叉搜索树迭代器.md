# 173、二叉搜索树迭代器
难度：mid

代码语言：cpp

题目网址：https://leetcode.cn/problems/binary-search-tree-iterator/description/
## 题解
### 方法一、队列
维护一个队列，调用构造函数时，依次往队列中加入中序遍历序列。调用hasNext时只需判断队列是否为空，调用next时，返回队头元素（并将其出队）即可

## 代码
C++

```cpp
class BSTIterator {
private:
    queue<int> q;
    void traverse(TreeNode* root) {
        if (root == NULL) return;
        traverse(root->left);
        q.push(root->val);
        traverse(root->right);
    }
public:
    BSTIterator(TreeNode* root) {
        traverse(root);
    }
    
    int next() {
        int val = q.front();
        q.pop();
        return val;
    }
    
    bool hasNext() {
        return !q.empty();
    }
};
```
