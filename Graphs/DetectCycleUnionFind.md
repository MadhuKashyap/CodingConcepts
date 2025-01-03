#### This method is used to detect cycle in undirected graph

1. Initially create subsets containing only a single node which are the parent of itself.
2. while traversing through the edges, if the two end nodes of the edge belongs to the same set then they form a cycle.
3. Otherwise, perform union to merge the subsets together. (make parent of 1 subset the parent of another subset)

![image](https://github.com/user-attachments/assets/f04d0e2e-8f6d-4da0-a75c-d6a5a4d668e1)

 We have an array parent[] which tells what element belongs to what subset
initially parent[] = {0,1,2} i.e. each element is a separate subset
Now process all edges one by one.
Edge 0-1: 
        => Find the subsets in which vertices 0 and 1 are. 
        => 0 and 1 belongs to subset 0 and 1.
        => Since they are in different subsets, take the union of them. 
        => For taking the union, either make node 0 as parent of node 1 or vice-versa. 
        => 1 is made parent of 0 (1 is now representative of subset {0, 1})
        => parent[] = {1, 1, 2}


Edge 1-2: 
        => 1 is in subset 1 and 2 is in subset 2.
        => Since they are in different subsets, take union.
        => Make 2 as parent of 1. (2 is now representative of subset {0, 1, 2})
        => parent[] = {1, 2, 2}


Edge 0-2: 
        => 0 is in subset 2 and 2 is also in subset 2. 
        => Because 1 is parent of 0 and 2 is parent of 1. So 0 also belongs to subset 2
        => Hence, including this edge forms a cycle. 


Therefore, the above graph contains a cycle.

```
package graph;

import java.util.ArrayList;
import java.util.List;

class Edge {
    int src, dest;
}
class Graph1 {
    int V;
    int E;
    List<Edge> edge;
    Graph1(int v, int e) {
        V = v;
        E = e;
        edge = new ArrayList<>(E);
    }
    void Union(int parent[], int x, int y)
    {
        parent[x] = y;
    }
    int find(int parent[], int i)
    {
        if (parent[i] == i)
            return i;
        return find(parent, parent[i]);
    }
    boolean isCycle(Graph1 graph)
    {
        int parent[] = new int[graph.V];

        // Initialize all subsets as single element sets
        for (int i = 0; i < graph.V; ++i)
            parent[i] = i;
        // Iterate through all edges of graph, find subset of both vertices of every edge, if both subsets
        // are same, then there is cycle in graph.
        for (int i = 0; i < graph.E; ++i) {
            int x = graph.find(parent, graph.edge.get(i).src);
            int y = graph.find(parent, graph.edge.get(i).dest);
            if(x == y)
                return true;
            graph.Union(parent, x, y);
        }
        return false;
    }
}
public class UnionFindCycleDetection {
    public static void main(String[] args) {
        int V = 3, E = 3;
        Graph1 graph = new Graph1(V, E);

        graph.edge.get(0).src = 0;
        graph.edge.get(0).dest = 1;

        // add edge 1-2
        graph.edge.get(1).src = 1;
        graph.edge.get(1).dest = 2;

        // add edge 0-2
        graph.edge.get(2).src = 0;
        graph.edge.get(2).dest = 2;
    }
}

```
