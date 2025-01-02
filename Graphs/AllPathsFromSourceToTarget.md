 https://leetcode.com/problems/all-paths-from-source-to-target/

```
public class AllPathsFromSourceToTarget {
    public static void main(String[] args) {
        int[][] graph = {{1,2},{3},{3},{}};
        System.out.println(allPathsSourceTarget(graph));
    }
    public static void func(int src, List<List<Integer>> res, List<Integer> list, int[][] graph) {
        if(src == graph.length - 1) {
            res.add(new ArrayList<>(list));
        }
        for(int i = 0; i < graph[src].length; i++) {
            list.add(graph[src][i]);
            func(graph[src][i], res, list, graph);
        }
        list.remove(list.size() - 1);
    }
    public static List<List<Integer>> allPathsSourceTarget(int[][] graph) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> list = new ArrayList<>();
        list.add(0);
        func(0, res, list, graph);
        return res;
    }
}
```
