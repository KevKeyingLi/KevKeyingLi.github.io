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

# Binary Tree Traversal
## Inorder
### Recursive
### Iterative with stack
### Iterative with Morrison?
## Preorder
## Postorder

# Tree/Graph Search
## BFS
## DFS