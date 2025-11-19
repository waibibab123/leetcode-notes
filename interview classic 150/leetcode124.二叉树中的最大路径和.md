# 124、二叉树中的最大路径和
hard

cpp
## 题解
后序遍历

维护一个全局变量res，当遍历到对应的节点时，更新：`res = max(res, root->val + left + right)`表示以root为根节点并且经过root的最大路径

然后返回：`max(0, max(left, right) + root->val)`，注意：
1. 为什么取left和right最大值，因为返回的这个值要被上层节点使用，就只能链接其中root左右子树的一个分支，而不是两个
2. 为什么要取0，如果这条分支最大也就凑出来一个小于0的数，那么还不如不要

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
    int res;
    int traverse(TreeNode* root) {
        if (root == NULL) return 0;
        int left = traverse(root->left);
        int right = traverse(root->right);
        res = max(root->val + left + right, res);
        return max(0, max(left, right) + root->val);
    }
    int maxPathSum(TreeNode* root) {
        res = INT_MIN;
        traverse(root);
        return res;
    }
};
```
