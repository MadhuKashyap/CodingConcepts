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
