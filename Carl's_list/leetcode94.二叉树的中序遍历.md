# 94、二叉树的中序遍历
题目网址：https://leetcode.cn/problems/binary-tree-inorder-traversal/description/

题目难度：easy

代码语言：cpp
## 方法一、递归法
比较简单，省略
## 方法二、非递归法
下面的方法适用于前序遍历和后续遍历，唯一不同的是入栈顺序

思路是用栈模拟这个递归过程，对于中序遍历，遍历顺序为左中右，由于栈是先进后出的数据结构，因此入栈顺序为右中左

如何知道当前栈顶元素是否需要加入遍历数组中？我们可以将这些元素上面加入一个NULL进行标记，具体见下面代码，这样的话，当栈顶元素为NULL时，下面的元素就需要加入遍历数组res中

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        if (root == NULL) return res;
        stack<TreeNode*> st;
        st.push(root);
        while (st.size()) {
            if (st.top() != NULL) {
                auto t = st.top();
                st.pop();
                if (t->right) st.push(t->right);
                st.push(t);
                st.push(NULL);
                if (t->left) st.push(t->left);
            } else {
                st.pop();
                res.push_back(st.top()->val);
                st.pop();
            }
        }
        return res;
    }
};
```
