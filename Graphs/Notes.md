### What is a Graph?

Graph is a non linear data structure with vertices as edges. It is represented as G(V, E).

### Types of graph
* Null Graph
A graph is known as a null graph if there are no edges in the graph.

* Trivial Graph
Graph having only a single vertex, it is also the smallest graph possible.
<img width="728" alt="image" src="https://github.com/user-attachments/assets/40fc5209-48d8-4bf5-90db-1e8ece5e3396">


* Undirected Graph
A graph in which edges do not have any direction. That is the nodes are unordered pairs in the definition of every edge. 

* Directed Graph
A graph in which edge has direction. That is the nodes are ordered pairs in the definition of every edge.

<img width="743" alt="image" src="https://github.com/user-attachments/assets/e4485b87-c3cf-4831-a356-e998ff10f528">


* Connected Graph
The graph in which from one node we can visit any other node in the graph is known as a connected graph. 

* Disconnected Graph
The graph in which at least one node is not reachable from a node is known as a disconnected graph.

<img width="743" alt="image" src="https://github.com/user-attachments/assets/ae06648e-e08c-43a0-a273-d41c875474f5">

* Complete Graph
The graph in which from each node there is an edge to each other node.

<img width="379" alt="image" src="https://github.com/user-attachments/assets/316a05fa-2e03-4ac4-b75c-5dc93b7a5575">

* Cyclic Graph
A graph containing at least one cycle is known as a Cyclic graph.
<img width="239" alt="image" src="https://github.com/user-attachments/assets/d40740ab-32b2-45e7-8ce0-0e508b654950">

* Directed Acyclic Graph
A Directed Graph that does not contain any cycle. 

* Bipartite Graph
A graph in which vertex can be divided into two sets such that vertex in each set does not contain any edge between them.

<img width="730" alt="image" src="https://github.com/user-attachments/assets/7b686f60-1d32-4d2d-bd4f-3fe3740ff20d">

### Representation of graphs
* Adjacency Matrix : the graph is stored in the form of the 2D matrix where rows and columns denote vertices. Each entry in the matrix represents the weight of the edge between those vertices.

<img width="484" alt="image" src="https://github.com/user-attachments/assets/b531b0dd-4225-43c7-9a4f-b71cb05c20c2">

* Adjacency List : This graph is represented as a collection of linked lists. There is an array of pointer which points to the edges connected to that vertex. 
<img width="728" alt="image" src="https://github.com/user-attachments/assets/dbd9febf-bd9c-45fe-a869-08b48c9b22df">

### Difference between Graph and trees

* Graph can have loop, trees can not have loops
* There can be ore than 1 path between edges in graph, only 1 path is possible in tree.

### Graph Traversal algorithms
* BFS : It begins with a node, then first traverses all its adjacent. Once all adjacent are visited, then their adjacent are traversed.

Applications : 
 ** Detect cycle in a directed graph 
 ** BFS can be used to find a topological ordering of the nodes in a directed acyclic graph
 ** 
* DFS : starts from a given source and explores all reachable vertices from the given source. 

```
public class Graph {
    List<List<Integer>> edges;
    boolean visited[];
    int V;
    Graph(int V) {
        this.V = V;
        edges = new ArrayList<>(V);
        visited = new boolean[V];
        for (int i = 0; i < V; i++) {
            edges.add(new ArrayList<>());
        }
    }
    public void addEdge(int u, int v) {
        edges.get(u).add(v);
    }
    public void bfs(int v) {
        Queue<Integer> q = new LinkedList<>();
        q.offer(v);
        visited[v] = true;
        while(!q.isEmpty()) {
            int top = q.poll();
            System.out.println(top);
            for(Integer i : edges.get(top)) {
                if(!visited[i]) {
                    visited[i] = true;
                    q.offer(i);
                }
            }
        }
    }
    public void dfs(int v) {
        visited[v] = true;
        System.out.println(v);
        for(Integer i : edges.get(v)) {
            if(!visited[i]) {
                dfs(i);
            }
        }
    }

    public static void main(String[] args) {
        Graph g = new Graph(4);
        g.addEdge(0, 1);
        g.addEdge(0, 2);
        g.addEdge(1, 3);
        g.addEdge(2, 1);
        g.bfs(0);
        Arrays.fill(g.visited, false);
        g.dfs(0);
    }
}

```

