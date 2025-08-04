# 617、合并二叉树
题目网址：https://leetcode.cn/problems/merge-two-binary-trees/description/

题目难度：easy

代码语言：cpp
## 题解
边界处理：如果root1为空，直接返回root2；同理，如果root2为空，直接返回root1

递归逻辑：直接使用前序遍历：
* 中：直接将两个root1的值和root2相加
* 左、右：通过递归得到root的左右子树

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
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        if (root1 == NULL) return root2;
        if (root2 == NULL) return root1;
        TreeNode* root = new TreeNode(0);
        if (root1) root->val += root1->val;
        if (root2) root->val += root2->val;
        root->left = mergeTrees(root1->left, root2->left);
        root->right = mergeTrees(root1->right, root2->right);
        return root;
    }
};
```
