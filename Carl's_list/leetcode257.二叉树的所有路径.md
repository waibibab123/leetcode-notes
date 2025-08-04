# 257、二叉树的所有路径
题目网址：https://leetcode.cn/problems/binary-tree-paths/

题目难度：easy

代码语言：cpp
## 题解
采用前序遍历方法，首先对于根节点，如果左右孩子均为空，那么就是叶子结点，就将这个结点加入路径path，并结束路径；如果左右孩子不为空，将这个结点加入路径path，但是不结束路径

对于左右结点，只需当其不为零时进行遍历即可

路径path如何维护？有两种方法：
* 一种是设置一个成员变量path，但是数据类型为vector<int>，以方便每次递归后的恢复现场，当遍历到叶子结点时，通过这个path数组直接构造出答案所需的string格式
* 另一种是直接将string类型的path以参数的形式传入，利用递归的性质避免手动恢复现场

第一种方式比较好理解，此处给出的是第二种方式的代码：

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
    vector<string> res;
    void traverse(TreeNode* root, string path) {
        if (root->left == NULL && root->right == NULL) {
            path += to_string(root->val);
            res.push_back(path);
            return;
        }
        else {
            path += (to_string(root->val) + "->");
        }
        if (root->left) traverse(root->left, path); 
        if (root->right) traverse(root->right, path);
    }
    vector<string> binaryTreePaths(TreeNode* root) {
        if (root == NULL) return res;
        traverse(root, "");
        return res;
    }
};
```
