**Problem**:
Given an undirected, unweighted graph, find the smallest cut, i.e., smallest number of edges that disconnects the graph into two components.

**Algorithm**:
- Initialize the contracted graph CG as a copy of the original graph
- While there are more than 2 vertices:
  - Pick a random edge `(u,v)` in the contracted graph.
  - Merge `u` and `v` into a single vertex and update the contracted graph
  - Remove self-loops
- Return cut represented by two vertices

![[Pasted image 20260424143238.png]]
