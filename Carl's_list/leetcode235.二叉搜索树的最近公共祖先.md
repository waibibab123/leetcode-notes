# 235、二叉搜索树的最近公共祖先
题目网址：https://leetcode.cn/problems/lowest-common-ancestor-of-a-binary-search-tree/submissions/639682444/

题目难度：mid

代码语言：cpp
## 题解
后序遍历，充分利用二叉搜索树的性质，首先，边界条件：root为空，直接返回空

如果root的值大于p、q的值，那么p、q一定在root左边，就将root->left传入函数进行递归

如果root的值小于p、q的值，那么p、q一定在root右边，就将root->right传入函数进行递归

如果上述不满足，说明root大于p、q中的一个、root小于p、q中的一个，那么root必然在p、q中间，又因为是后序遍历，所以是从下往上的，那么root此时是p、q公共祖先且是最深的，直接返回root

C++
```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == NULL) return NULL;
        if (root->val > p->val && root->val > q->val) {
            TreeNode* left = lowestCommonAncestor(root->left, p, q);
            return left;
        }
        if (root->val < p->val && root->val < q->val) {
            TreeNode* right = lowestCommonAncestor(root->right, p, q);
            return right;
        }
        return root;
    }
};
```
