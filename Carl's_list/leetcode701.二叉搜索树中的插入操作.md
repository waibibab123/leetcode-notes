# 701、二叉搜索树中的插入操作
题目网址：https://leetcode.cn/problems/insert-into-a-binary-search-tree/submissions/639872284/

题目难度：mid

代码语言：cpp
## 题解
如果root本身为空，直接创建一个值为val的节点并返回即可

如果root的值小于val，则将val插入root右子树；否则，插入左子树。最后返回root

C++
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
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if (root == NULL) return new TreeNode(val);
        if (val < root->val) root->left = insertIntoBST(root->left, val);
        if (val > root->val) root->right = insertIntoBST(root->right, val);
        return root;
    }
};
```
