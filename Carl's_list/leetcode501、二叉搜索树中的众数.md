# 501、二叉搜索树中的众数
题目网址：https://leetcode.cn/problems/find-mode-in-binary-search-tree/submissions/639293420/

题目难度：easy

代码语言：cpp
## 题解
看到二叉搜索树，利用其中序遍历序列有序的性质，额外定义一个前驱结点指针pre、答案数组res以及两个整数cnt、max_cnt分别记录当前节点的频率以及目前遍历到的最大频率

每次遍历的逻辑是：1.更新cnt 2.更新res 3.更新pre
* 更新cnt：
  * 如果pre为空，直接cnt = 1，表示当前root节点频率为1（仅遍历了一个）
  * 如果pre不为空，且pre的值与root的值相同，说明root节点的频率比pre节点的频率多一，因此cnt = cnt + 1
  * 如果pre不为空，但pre的值与root的值不同，说明需要重新记录cnt，因此cnt = 1
* 更新res：
  * 如果cnt == max_cnt，说明目前存在多个众数，直接向res中加入root节点的值即可
  * 如果cnt > max_cnt，说明目前出现了一个比之前遍历到频率最高的节点的频率还高的节点，因此需要清空res并更新max_cnt，最后向res中放入新的root
* 更新pre：
  * pre = root

C++
```cpp/**
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
    vector<int> res;
    TreeNode* pre;
    int cnt = 0;
    int max_cnt = 0;
    void traverse(TreeNode* root) {
        if (root == NULL) return;
        traverse(root->left);
        if (pre == NULL) {
            cnt = 1;
        } else if (pre->val == root->val) {
            cnt ++ ;
        } else {
            cnt = 1;
        }
        if (cnt > max_cnt) {
            res.clear();
            res.push_back(root->val);
            max_cnt = cnt;
        } else if (cnt == max_cnt) res.push_back(root->val);
        pre = root;
        traverse(root->right);
    }
    vector<int> findMode(TreeNode* root) {
        traverse(root);
        return res;
    }
};
```
