### Spanning Tree
 
1. A spanning tree is a connected undirected graph with no cycles.
2. A spanning tree has the same number of vertices as the graph .
3. The total number of edges in a spanning tree is \(n-1\), where \(n\) is the number of vertices in the graph.

### Minimum spanning tree
A minimum spanning tree (MCST) is a spanning tree with the smallest edge weight sum.

Kruskal's algorithm
```
public int minCostConnectPoints(int[][] points) {
        int n = points.length;
        List<List<Integer>> edges = new ArrayList<>();

        // Generate all edges with their costs
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int cost = Math.abs(points[i][0] - points[j][0]) + Math.abs(points[i][1] - points[j][1]);
                edges.add(Arrays.asList(i, j, cost));
            }
        }

        edges.sort((a, b) -> a.get(2) - b.get(2));

        // Union-Find setup
        int[] parent = new int[n];
        int[] rank = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
        }

        // Kruskal's algorithm
        int minCost = 0;
        int edgesUsed = 0;

        for (List<Integer> edge : edges) {
            int u = edge.get(0);
            int v = edge.get(1);
            int cost = edge.get(2);

            if (find(parent, u) != find(parent, v)) {
                union(parent, rank, u, v);
                minCost += cost;
                edgesUsed++;
                if (edgesUsed == n - 1) break; // Minimum Spanning Tree complete
            }
        }

        return minCost;
    }

    // Find with path compression
    private int find(int[] parent, int i) {
        if(parent[i] == i)
            return i;
        return find(parent, parent[i]);
    }

    // Union by rank
    // This is used to keep the height of the resultant tree as small as possible
    // It makes sure that a tree with bigger height is made the parent of a tree with smaller height
    private void union(int[] parent, int[] rank, int u, int v) {
        int rootU = find(parent, u);
        int rootV = find(parent, v);

        if (rootU != rootV) {
            if (rank[rootU] > rank[rootV]) {
                parent[rootV] = rootU;
            } else if (rank[rootU] < rank[rootV]) {
                parent[rootU] = rootV;
            } else {
                parent[rootV] = rootU;
                rank[rootU]++;
            }
        }
    }
```
