# Binary Search
https://github.com/labuladong/fucking-algorithm/blob/master/%E7%AE%97%E6%B3%95%E6%80%9D%E7%BB%B4%E7%B3%BB%E5%88%97/%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE%E8%AF%A6%E8%A7%A3.md

This is good for solving:
* find target/insertion point/start&end point of a interval


## `while (l < r)`
`l < r` represents half open half close interval. I prefer to use left open right closed interval: `l = mid + 1`. 


Following is a snippet for finding target/insertion point in non-duplicated sorted array. 
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

## `while (l <= r)`
*  `while (l <= r)` is for a closed interval: `[l, r]`, element `l` and `r` are potential target
* the terminate condition is `l == r + 1`. b/c this means the interval doesn't contain any potential target
* To make the range qualify a closed interval， every loop we do `l = mid + 1` or `r = mid - 1`;


## Variations
Base scenario: find element in  

* find boundary of a range/target
* with duplication
* with rotated

## Mistakes
* array
    - index out of bound
    - range of elements
    - duplication
    - order of elements
* coding mistake
    - use `l`, `r`, `mid` as element, instead of `nums[l]`...




# Sorting
## Merge Sort
## Heap Sort
## Quick Sort
### Quick select
Two sub-routines:
* Partition: given a range, select one element as pivot(arbitrarily last one, or a random one.) Move elements smaller than it to it's left by swapping
* kthSmallest(arr, l, r, k): get the index of pivot element from partition, if it matches k, return; if not, search for k in new sub-range. 

```
class GFG { 
    // Standard partition process of QuickSort. 
    // It considers the last element as pivot 
    // and moves all smaller element to left of 
    // it and greater elements to right 
    public static int partition(Integer[] arr, int l, 
                                int r) 
    { 
        int x = arr[r], i = l; 
        for (int j = l; j <= r - 1; j++) { 
            if (arr[j] <= x) { 
                // Swapping arr[i] and arr[j] 
                int temp = arr[i]; 
                arr[i] = arr[j]; 
                arr[j] = temp; 
  
                i++; 
            } 
        } 
  
        // Swapping arr[i] and arr[r] 
        int temp = arr[i]; 
        arr[i] = arr[r]; 
        arr[r] = temp; 
  
        return i; 
    } 
  
    // This function returns k'th smallest element 
    // in arr[l..r] using QuickSort based method. 
    // ASSUMPTION: ALL ELEMENTS IN ARR[] ARE DISTINCT 
    public static int kthSmallest(Integer[] arr, int l, 
                                  int r, int k) 
    { 
        // If k is smaller than number of elements 
        // in array 
        if (k > 0 && k <= r - l + 1) { 
            // Partition the array around last 
            // element and get position of pivot 
            // element in sorted array 
            int pos = partition(arr, l, r); 
  
            // If position is same as k 
            if (pos - l == k - 1) 
                return arr[pos]; 
  
            // If position is more, recur for 
            // left subarray 
            if (pos - l > k - 1) 
                return kthSmallest(arr, l, pos - 1, k); 
  
            // Else recur for right subarray 
            return kthSmallest(arr, pos + 1, r, k - pos + l - 1); 
        } 
  
        // If k is more than number of elements 
        // in array 
        return Integer.MAX_VALUE; 
    } 
  
    // Driver program to test above methods 
    public static void main(String[] args) 
    { 
        Integer arr[] = new Integer[] { 12, 3, 5, 7, 4, 19, 26 }; 
        int k = 3; 
        System.out.print("K'th smallest element is " + kthSmallest(arr, 0, arr.length - 1, k)); 
    } 
} 

```
## Patience Sort
# substrings
https://leetcode.com/problems/minimum-window-substring/discuss/26808/Here-is-a-10-line-template-that-can-solve-most-'substring'-problems

# Sliding Window & Two Pointers
base case two pointers, right pointer extends, left pointer retracts based on conditions. 

[209. Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/submissions/)

## The simple template
```
        ...
        int l = 0, r = 0;
        // [ l, r): left closed, right open interval
        //l is next to delete, r is next to add
        //len of interval: r - l
        int sum = 0;
        while (r < nums.length) {//conditioned on right pointer
            //The operation of extending right pointer, one at a time
            //e.g. sum += nums[r];
            r++;
            //test condition and retract left pointer
            while (l < r && sum - nums[l] >= s) {
                //The operation of retract left pointer
                //e.g. sum -= nums[l];
                l++;
                //Additional logics if needed
            }
            // additional logics for each step.
            ...
            //register a local solution
            //e.g.
            // minLen = Math.min(minLen, r - l);
        }
        ...

```
## The complex template - TODO
https://leetcode.com/problems/find-all-anagrams-in-a-string/discuss/92007/sliding-window-algorithm-template-to-solve-all-the-leetcode-substring-search-problem 
## Common Issues
* Mistake: use index value `l` `r` in place of real values `nums[l]`, `num[r]`

## Problems
* [904. Fruit Into Baskets](https://leetcode.com/problems/fruit-into-baskets/): basic sliding window
* [1248 Count Number of Nice Subarrays](https://leetcode.com/problems/count-number-of-nice-subarrays/): good basic sliding window with a simple/nice twist
* [1234 Replace the Substring for Balanced String](https://leetcode.com/problems/replace-the-substring-for-balanced-string/): good basic sliding window with a interesting twist
* [1004 Max Consecutive Ones III](https://leetcode.com/problems/max-consecutive-ones-iii/) good basic sliding window with a simple/nice twist
* [930 Binary Subarrays With Sum](https://leetcode.com/problems/binary-subarrays-with-sum/): basic+tricky twist
* [992 Subarrays with K Different Integers](https://leetcode.com/problems/subarrays-with-k-different-integers/): Hard+classic
* [862 Shortest Subarray with Sum at Least K](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/): Hard+interesting
* [209 Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/): basic
* [438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/): 

Two similar problems, not so much about sliding window
* [30. Substring with Concatenation of All Words](https://leetcode.com/problems/substring-with-concatenation-of-all-words/) hard+low rating
* [76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) hard good
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
Tree & graph basics
Tree
* n node with n - 1 edges
* path from one node to other is unique
* tree leaves have 1 connected edge

Graph
* 


Difference between tree and graph
* because there may be more than one path connecting two nodes, `visited` set is often used so each node is visited only once.
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
# Backtracking
backtracking is a subset of dfs, tree/graph traversal problems

The path of backtracking is a multi-branch decision tree, the process of backtracking is 
* creating new node when visiting, removing node after visit.
* pre-order decision making + post-order decision undo

Similar to DP, where at each step we need to be clear of `state`, `decision`, and `base case`, for backtracking we need similar things `current decision path/state of all decisions made`, `list of options, next steps to choose from`, `terminate condition, base case`

Similar problems
* backtracking
* subsets
* permutation
* combination

A leetcode discussion: https://leetcode.com/problems/permutations/discuss/18239/A-general-approach-to-backtracking-questions-in-Java-(Subsets-Permutations-Combination-Sum-Palindrome-Partioning)


## Key points:
### Types
* permutation: order of elements is considered, think of a list
* combination: order of elements is not considered, think of a set
* Note: Both permutation and combination can allow or not allow for duplicate elemenets
### basic logic

[labuladong](https://labuladong.gitbook.io/algo/di-ling-zhang-bi-du-xi-lie/hui-su-suan-fa-xiang-jie-xiu-ding-ban)
input
* the original data source
* information of current state: 
    - an index of next element to visit
    - a set of elements used
    - an array/hashmap visited[]
* options for next step
    - an index of next element to visit
    - use all the data in the orignial data source(duplication is allowed)
* a result collection for storing the results, as the recursion happens

Internal logics
* handle base case, add result to result collection if needed. 
* a for loop trying out all possible options for current step
    - apply one option
    - recurse to next level
    - once recursion returns, undo this option and move on to next iteration of loop for next option


In other words:(TODO consolidate these two)
1. at each recursion, pass 
    * *results*: the collection that contains final results
    * *current temp*: a temp state of one of the final results
    * *the candidate pool* + *some way of determining what elements can be used*
        - a set/list of remaining elements: this need to be updated/regenerated for each recursion, 
        - original candidate array/list + a index if list can be processed in order
        - original candidate array/list + an extra array `used` indicating what elements are used): versitale
    * *other relevant information*: extra info needed for processing, for example a target in combination sum. 
2. Only add a final result into *results* collection when a base case is reached. All other layers of recursion are for building up the *temp result*
### Failure points/Clarification points
* duplication in input data, and if result allow duplication
    - duplication in input is solved by sorting, and every time comparing with previous one
    - if result does allow duplicate
* how to dedup? 
    - use a boolean array to track visited/used: `new boolean[nums.length]`(Permutation ii)
    - sort and use a condition, this is good if we are scanning with an index. (subset ii)
### The math
[Permutations Combinations Factorials & Probability](https://www.youtube.com/watch?v=TBnPkKxXPu8&ab_channel=Mario%27sMathTutoring)

### Special attention
### BFS solution
A note mentioned "DFS is well-known to solve this, but you should understand the BFS solution, which is more generic to be applied to different follow-ups"
## Problems
https://leetcode.com/problems/subsets/
Subsets II (contains duplicates) : https://leetcode.com/problems/subsets-ii/
Permutations : https://leetcode.com/problems/permutations/
Permutations II (contains duplicates) : https://leetcode.com/problems/permutations-ii/
Combination Sum : https://leetcode.com/problems/combination-sum/
Combination Sum II (can't reuse same element) : https://leetcode.com/problems/combination-sum-ii/
Palindrome Partitioning : https://leetcode.com/problems/palindrome-partitioning/



# Monotone Stack
There is another note for Mono-stack. preps/algos/Monotone Stack.md
## Problems
https://leetcode.com/problems/sum-of-subarray-minimums/
## Explanations
https://github.com/labuladong/fucking-algorithm/blob/master/%E6%95%B0%E6%8D%AE%E7%BB%93%E6%9E%84%E7%B3%BB%E5%88%97/%E5%8D%95%E8%B0%83%E6%A0%88.md
https://labuladong.gitbook.io/algo-en/

# Narrower Categories...
## Single numbers: 
https://leetcode.com/problems/single-number-ii/discuss/43295/Detailed-explanation-and-generalization-of-the-bitwise-operation-method-for-single-numbers for generalized solution
        //https://leetcode.com/problems/single-number-ii/discuss/43297/Java-O(n)-easy-to-understand-solution-easily-extended-to-any-times-of-occurance

