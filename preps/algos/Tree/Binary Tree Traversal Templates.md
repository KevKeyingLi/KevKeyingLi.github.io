## Inorder Traversal
```
    ...
    Stack<TreeNode> stack = new Stack<TreeNode>();
    TreeNode cur = root;

    while(cur!=null || !stack.empty()){
        while(cur!=null) {
            stack.add(cur);
            cur = cur.left;
        }
        cur = stack.pop();
        //Do something
        cur = cur.right;
    }
    ...
```
Important points:
* `while(cur!=null || !stack.empty())`
* at each node
    - we first push all the left path into the stack: `while(cur!=null)`
    - then we pop a node, record it, and go to it's right subtree. 
