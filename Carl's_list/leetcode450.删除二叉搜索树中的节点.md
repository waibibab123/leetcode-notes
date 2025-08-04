# 450、删除二叉搜索树的节点
题目网址：https://leetcode.cn/problems/delete-node-in-a-bst/

题目难度：mid

代码语言：cpp
## 题解
如果要删除一个二叉搜索树的结点，分为三种情况：

* 这个节点无孩子结点，直接删
* 这个节点有左/右子树，删完之后将左/右子树接在这个节点的父亲结点上
* 这个节点既有左子树，又有右子树，首先要将左子树接在右子树的最左下处，然后将右子树根节点接在这个节点的父亲结点上

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
    TreeNode* deleteNode(TreeNode* root, int key) {
        if (root == NULL) return NULL;
        if (root->val == key) {
            if (root->left == NULL && root->right == NULL) return NULL;
            if (root->left != NULL && root->right == NULL) return root->left;
            if (root->left == NULL && root->right != NULL) return root->right;
            TreeNode* cur = root->right;
            while (cur->left != NULL) cur = cur->left;
            cur->left = root->left;
            return root->right;
        }
        else if (root->val < key) root->right = deleteNode(root->right, key);
        else root->left = deleteNode(root->left, key);
        return root;
    }
};
```
