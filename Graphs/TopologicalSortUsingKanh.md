```
/**
 * Kanh's algorithm not only prints Topological sort for a DAG but also detects if a graph contains cycle or not
 */
public class TopologicalSortKanh {
    public static void main(String[] args) {
        Graph g = new Graph(4);

    }
    public static int[] topoKanh(Graph g) {
        int[] indegree = new int[g.V];
        int[] result = new int[g.V];
        int index = 0;
        for(int i = 0; i < g.V; i++) {
            for(Integer it : g.edges.get(i)) {
                indegree[it]++;
            }
        }
        Queue<Integer> q = new LinkedList<>();
        for(int i = 0 ; i < g.V; i++) {
            if(indegree[i] == 0)
            q.offer(i);
        }
        while(!q.isEmpty()) {
            int top = q.poll();
            result[index++] = top;
            for(Integer it : g.edges.get(top)) {
                indegree[it]--;
                if(indegree[it] == 0)
                    q.offer(it);
            }
        }
        if(index != g.V) {
            System.out.println("Graph contains cycle");
            return new int[]{};
        }
        return result;
    }
}
```
