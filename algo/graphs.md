### DFS with stack

Depth-first search is an algorithm for traversing or searching tree or graph data structures. The algorithm **starts at the root node** (selecting some arbitrary node as the root node in the case of a graph) and explores as far as possible along each branch before backtracking. So the basic idea is to start from the root or any arbitrary node and mark the node and move to the adjacent unmarked node and continue this loop until there is no unmarked adjacent node. Then backtrack and check for other unmarked nodes and traverse them. Finally print the nodes in the path.

Depth First Traversal can be **used to detect a cycle** in a Graph. DFS for a connected graph **produces a tree**. There is a cycle in a graph only if there is a back edge present in the graph. A back edge is an edge that is joining a node to itself (self-loop) or one of its ancestor in the tree produced by DFS. 
To find the back edge to any of its ancestor keep a visited array and if there is a back edge to any visited node then there is a loop and return true.

### BFS with queue

