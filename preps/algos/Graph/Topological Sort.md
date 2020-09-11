Only possible in a DAG (Directed Acyclic Graph)
Normal DFS/BFS won't work, but 


## Applications: all kinds of dependency problems
* build systems, package tools
* task scheduling
* pre-requisite problems. e.g. course structure...

Topological sort can also be seen as related to dead lock problem, since both are non-cyclic-dependency scenarios. 


## Implementation Gists
* use DFS, a stack, an array/hashmap/hashset storing visited state. 
* use DFS to find a leaf node, which doesn't have 0 out degree, that's where we find a starting point to store in the stack. 
* everytime a node is a leaf, or it's children are all visited, we add it to the stack. Thus making sure that anything we add to stack, it's children are already in the stack.

DFS: time O(V+E)
