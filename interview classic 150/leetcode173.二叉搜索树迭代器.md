# 173、二叉搜索树迭代器
mid

cpp
## 题解
可以在构造函数中，提前中序遍历一遍，把结点记下来，然后后面用索引进行访问

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
class BSTIterator {
private:
    vector<int> nodes;
    int index = 0;
    void traverse(TreeNode* root) {
        if (root == NULL) return;
        traverse(root->left);
        nodes.push_back(root->val);
        traverse(root->right);
    }
public:
    BSTIterator(TreeNode* root) {
        traverse(root);
    }
    
    int next() {
        return nodes[index ++ ];
    }
    
    bool hasNext() {
        return index != nodes.size();
    }
};

/**
 * Your BSTIterator object will be instantiated and called as such:
 * BSTIterator* obj = new BSTIterator(root);
 * int param_1 = obj->next();
 * bool param_2 = obj->hasNext();
 */
```
