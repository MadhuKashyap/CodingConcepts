 ```
public class TopologicalSort {
    public static void main(String[] args) {
        Graph g = new Graph(4);
        g.addEdge(0, 2);
        g.addEdge(0, 1);
        g.addEdge(2, 1);
        g.addEdge(3, 1);
        g.addEdge(3, 3);
        topoSort(g);
    }
    public static void topoSort(Graph g) {
        Stack<Integer> st = new Stack<>();
        for(int i = 0; i < g.V; i++) {
            if(!g.visited[i])
                topoSortUtil(i, g, st);
        }
        while(!st.isEmpty()) {
            System.out.println(st.pop());
        }
    }
    public static void topoSortUtil(int v, Graph g, Stack<Integer> st) {
        g.visited[v] = true;
        for(Integer i : g.edges.get(v)) {
            if(!g.visited[i])
                topoSortUtil(i, g, st);
        }
        st.push(v);
    }
}
```
