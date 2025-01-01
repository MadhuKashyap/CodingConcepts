 ```
public class DetectCycleInGraph {
    public static void main(String[] args) {
        Graph g = new Graph(4);
        g.addEdge(0, 2);
        g.addEdge(0, 1);
        g.addEdge(2, 1);
        g.addEdge(3, 1);
        g.addEdge(3, 3);
        System.out.println(detectCycle(g));
    }
    public static boolean hasCycle(int v, Graph g, boolean recursion[]) {
        g.visited[v] = true;
        recursion[v] = true;
        for(Integer i : g.edges.get(v)) {
            if(!g.visited[i] && hasCycle(i, g, recursion))
                return true;
            else if(recursion[i])
                return true;
        }
        recursion[v] = false;
        return false;
    }
    public static boolean detectCycle(Graph g) {
        boolean recursion[] = new boolean[g.V];
        for(int i = 0; i < g.V; i++) {
            if(hasCycle(i, g, recursion))
                return true;
        }
        return false;
    }
}
```
