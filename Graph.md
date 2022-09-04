# Graphs

Here is some common terminology used when working with Graphs:

* Vertex - A vertex, also called a “node”, is a data object that can have zero or more adjacent vertices.
* Edge - An edge is a connection between two nodes.
* Neighbor - The neighbors of a node are its adjacent nodes, i.e., are connected via an edge.
* Degree - The degree of a vertex is the number of edges connected to that vertex.

## Directed vs Undirected

### Undirected Graphs

An Undirected Graph is a graph where each edge is undirected or bi-directional. This means that the undirected graph does not move in any direction.

### Directed Graphs (Digraph)
A Directed Graph also called a Digraph is a graph where every edge is directed.

Unlike an undirected graph, a Digraph has direction. Each node is directed at another node with a specific requirement of what node should be referenced next.

## Complete vs Connected vs Disconnected
There are many different types of graphs. This depends on how connected the graphs are to other node/vertices.

The three different types are completed, connected, and disconnected.

### Complete Graphs
A complete graph is when all nodes are connected to all other nodes.

Take a close look at each of the vertices in the graph above. Do you notice that each vertex is actually connected to every other node on the graph? That is what makes it a complete graph.

### Connected
A connected graph is graph that has all of vertices/nodes have at least one edge.

### Disconnected
A disconnected graph is a graph where some vertices may not have edges.

Acyclic vs Cyclic
In addition to undirected and directed graphs, we also have acyclic and cyclic graphs.

## Acyclic Graph
### An acyclic graph is a directed graph without cycles.

### A cycle is when a node can be traversed through and potentially end up back at itself.

Here is an example of 3 acyclic graphs:

Cyclic Graphs
A Cyclic graph is a graph that has cycles.

A cycle is defined as a path of a positive length that starts and ends at the same vertex.