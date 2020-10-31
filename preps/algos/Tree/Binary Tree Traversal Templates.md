# Traversal
https://leetcode.com/problems/binary-tree-postorder-traversal/discuss/45551/Preorder-Inorder-and-Postorder-Iteratively-Summarization

## Binary Tree Inorder Traversal
```
    ...
    Deque<TreeNode> stack = new Stack<TreeNode>();
    TreeNode cur = root;

    while(cur!=null || !stack.isEmpty()){
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
* `while(cur!=null || !stack.isEmpty())`
* at each node
    - we first push all the left path into the stack: `while(cur!=null)`
    - then we pop a node, record it, and go to it's right subtree. 
* with `!stack.isEmpty()` we allow `cur` to be `null`, thus, avoiding a lot of problem.
* cur always points to the element to be pushed into the stack
* if cur == null, this means a subtree has finished, we pop one node from stack
TODO read algorithm book on this
## Preorder Traversal
Quite similar to inorder:

```
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> results = new LinkedList<>();
        Deque<TreeNode> stack = new LinkedList<>();
        TreeNode cur = root;
        while (cur != null || !stack.isEmpty()) {
            while (cur != null) {
                results.add(cur.val);
                stack.push(cur);
                cur = cur.left;
            }
            cur = stack.pop();
            cur = cur.right;
        }
        return results;
    }
```

## Postorder Traversal

	
Binary Tree Level Order Traversal

# Variants:
## Constructing trees from traversal:
Construct Binary Tree from Preorder and Inorder Traversal
Construct Binary Tree from Inorder and Postorder Traversal 

[1028. Recover a Tree From Preorder Traversal](https://leetcode.com/problems/recover-a-tree-from-preorder-traversal) **Hard**

297 Serialize and Deserialize Binary Tree
449 Serialize and Deserialize BST