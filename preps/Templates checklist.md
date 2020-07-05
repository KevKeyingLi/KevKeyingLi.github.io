# Binary Search
## `while (l < r)`
This requires moving left/low pointer to `mid+1` everytime. Following is a snippet for finding target/insertion point in none duplicated sorted array. 
```
    public int searchInsert(int[] nums, int target) {
        if (nums == null || nums.length == 0)
            return 0;
        if (target <= nums[0])
            return 0;
        if (target > nums[nums.length - 1])
            return nums.length;
        int lo = 0;
        int hi = nums.length - 1;
        while (lo < hi) {
            int mid = lo + (hi - lo)/2;
            if (nums[mid] == target)
                return mid;
            else if (nums[mid] < target)
                lo = mid + 1;
            else
                hi = mid;
        }
        return lo;
    }
```

This is good for solving:
* find target/insertion point


# Sorting
## Merge Sort
## Heap Sort
## Quick Sort
## Patience Sort

# Sliding Window

# Binary Tree
## Traversal
### Inorder
#### Recursive
#### Iterative with stack
#### Iterative with Morrison?
### Preorder
### Postorder
## Other typical problems
### Kth Smallest Element in a BST
[Leetcode 230. Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

Augmented data structure: add count at each node. 
# Tree/Graph Search
## BFS
## DFS


## Disjointed Set & Union Find
* A disjoint-set data structure is a data structure that keeps track of a set of elements partitioned into a number of disjoint (non-overlapping) subsets.
* A union-find algorithm is an algorithm that performs two useful operations on such a data structure:
    - **Find**: Determine which subset a particular element is in. This can be used for determining if two elements are in the same subset.
    - **Union**: Join two subsets into a single subset.

### Usage:
* check whether an undirected graph contains cycle or not (vs Detect Cycle in a Directed Graph by DFS)
### Ways of improvement
Union by Rank and Path Compression: https://www.geeksforgeeks.org/union-find-algorithm-set-2-union-by-rank/

### Templates and Examples

```
// Naive implementation of find 
int find(int parent[], int i) 
{ 
    if (parent[i] == -1) 
        return i; 
    return find(parent, parent[i]); 
} 
   
// Naive implementation of union() 
void Union(int parent[], int x, int y) 
{ 
    int xset = find(parent, x); 
    int yset = find(parent, y); 
    parent[xset] = yset; 
} 
```

Solution for [547. Friend Circles](https://leetcode.com/problems/friend-circles/discuss/101336/Java-solution-Union-Find)
```
public class Solution {
    class UnionFind {
        private int count = 0;
        private int[] parent, rank;
        
        public UnionFind(int n) {
            count = n;
            parent = new int[n];
            rank = new int[n];
            for (int i = 0; i < n; i++) {
                parent[i] = i;
            }
        }
        
        public int find(int p) {
        	while (p != parent[p]) {
                parent[p] = parent[parent[p]];    // path compression by halving
                p = parent[p];
            }
            return p;
        }
        
        public void union(int p, int q) {
            int rootP = find(p);
            int rootQ = find(q);
            if (rootP == rootQ) return;
            if (rank[rootQ] > rank[rootP]) {
                parent[rootP] = rootQ;
            }
            else {
                parent[rootQ] = rootP;
                if (rank[rootP] == rank[rootQ]) {
                    rank[rootP]++;
                }
            }
            count--;
        }
        
        public int count() {
            return count;
        }
    }
    
    public int findCircleNum(int[][] M) {
        int n = M.length;
        UnionFind uf = new UnionFind(n);
        for (int i = 0; i < n - 1; i++) {
            for (int j = i + 1; j < n; j++) {
                if (M[i][j] == 1) uf.union(i, j);
            }
        }
        return uf.count();
    }
}
```

```
public class Solution {
    int rows, cols;
    
    public void solve(char[][] board) {
        if(board == null || board.length == 0) return;
        
        rows = board.length;
        cols = board[0].length;
        
        // last one is dummy, all outer O are connected to this dummy
        UnionFind uf = new UnionFind(rows * cols + 1);
        int dummyNode = rows * cols;
        
        for(int i = 0; i < rows; i++) {
            for(int j = 0; j < cols; j++) {
                if(board[i][j] == 'O') {
                    if(i == 0 || i == rows-1 || j == 0 || j == cols-1) {
                        uf.union(node(i,j), dummyNode);
                    }
                    else {
                        if(i > 0 && board[i-1][j] == 'O')  uf.union(node(i,j), node(i-1,j));
                        if(i < rows-1 && board[i+1][j] == 'O')  uf.union(node(i,j), node(i+1,j));
                        if(j > 0 && board[i][j-1] == 'O')  uf.union(node(i,j), node(i, j-1));
                        if(j < cols-1 && board[i][j+1] == 'O')  uf.union(node(i,j), node(i, j+1));
                    }
                }
            }
        }
        
        for(int i = 0; i < rows; i++) {
            for(int j = 0; j < cols; j++) {
                if(uf.isConnected(node(i,j), dummyNode)) {
                    board[i][j] = 'O';
                }
                else {
                    board[i][j] = 'X';
                }
            }
        }
    }
    
    int node(int i, int j) {
        return i * cols + j;
    }
}

class UnionFind {
    int [] parents;
    public UnionFind(int totalNodes) {
        parents = new int[totalNodes];
        for(int i = 0; i < totalNodes; i++) {
            parents[i] = i;
        }
    }
    
    void union(int node1, int node2) {
        int root1 = find(node1);
        int root2 = find(node2);
        if(root1 != root2) {
            parents[root2] = root1;
        }
    }
    
    int find(int node) {
        while(parents[node] != node) {
            parents[node] = parents[parents[node]];
            node = parents[node];
        }
        
        return node;
    }
    
    boolean isConnected(int node1, int node2) {
        return find(node1) == find(node2);
    }
}
```

# Monotone Stack
## Problems
https://leetcode.com/problems/sum-of-subarray-minimums/
## Explanations
https://github.com/labuladong/fucking-algorithm/blob/master/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E7%B3%BB%E5%88%97/%E5%8D%95%E8%B0%83%E6%A0%88.md
https://labuladong.gitbook.io/algo-en/

# Narrower Categories...
## Single numbers: 
https://leetcode.com/problems/single-number-ii/discuss/43295/Detailed-explanation-and-generalization-of-the-bitwise-operation-method-for-single-numbers for generalized solution
        //https://leetcode.com/problems/single-number-ii/discuss/43297/Java-O(n)-easy-to-understand-solution-easily-extended-to-any-times-of-occurance

