[二叉搜索树与双向链表](https://www.nowcoder.com/practice/947f6eb80d944a84850b0538bf0ec3a5?tpId=13&tqId=11179&tPage=2&rp=2&ru=/ta/coding-interviews&qru=/ta/coding-interviews/question-ranking)

this problem is about *traverse a tree* and *use a stack*.

stack and queue are good container to traserve some orders.

here are the solution of mine:

``` C++
/*
struct TreeNode {
	int val;
	struct TreeNode *left;
	struct TreeNode *right;
	TreeNode(int x) :
			val(x), left(NULL), right(NULL) {
	}
};*/
class Solution {
public:
    void recursion(TreeNode* cur , stack<TreeNode*>& s) {
        if(cur->left) recursion(cur->left , s);
        s.push(cur);
        if(cur->right) recursion(cur->right , s);
    }
    
    TreeNode* Convert(TreeNode* pRootOfTree)
    {
        stack<TreeNode*> s;
        if(pRootOfTree) recursion(pRootOfTree , s);
        TreeNode* cur = NULL;
        while(!s.empty()) {
            cur = s.top();
            s.pop();
            if(s.empty()) break;
            cur->left = s.top();
            s.top()->right = cur;
        }
        return cur;
    }
};

```
