# 114、二叉树展开为链表
mid

cpp
## 题解
链表的顺序为前序遍历的顺序，但如果使用头插法构建链表，顺序是相反的，所以我们可以遍历前序遍历的逆顺序：

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
    TreeNode* head = NULL;
    void flatten(TreeNode* root) {
        if (root == NULL) return;
        flatten(root->right);
        flatten(root->left);
        root->right = head;
        root->left = NULL;
        head = root;
    }
};
```
