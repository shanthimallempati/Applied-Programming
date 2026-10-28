import java.util.*;

class Solution {
    public int[] sortItems(int n, int m, int[] group,
                           List<List<Integer>> beforeItems) {

        // Give each ungrouped item its own group
        for (int i = 0; i < n; i++) {
            if (group[i] == -1) {
                group[i] = m++;
            }
        }

        List<List<Integer>> itemGraph = new ArrayList<>();
        List<List<Integer>> groupGraph = new ArrayList<>();

        for (int i = 0; i < n; i++) {
            itemGraph.add(new ArrayList<>());
        }

        for (int i = 0; i < m; i++) {
            groupGraph.add(new ArrayList<>());
        }

        int[] itemDegree = new int[n];
        int[] groupDegree = new int[m];

        for (int i = 0; i < n; i++) {
            for (int prev : beforeItems.get(i)) {
                itemGraph.get(prev).add(i);
                itemDegree[i]++;

                if (group[prev] != group[i]) {
                    groupGraph.get(group[prev]).add(group[i]);
                    groupDegree[group[i]]++;
                }
            }
        }

        List<Integer> itemOrder = topoSort(itemGraph, itemDegree);
        List<Integer> groupOrder = topoSort(groupGraph, groupDegree);

        if (itemOrder.size() != n || groupOrder.size() != m) {
            return new int[0];
        }

        Map<Integer, List<Integer>> groupedItems = new HashMap<>();

        for (int item : itemOrder) {
            groupedItems.computeIfAbsent(
                group[item], k -> new ArrayList<>()
            ).add(item);
        }

        int[] result = new int[n];
        int index = 0;

        for (int g : groupOrder) {
            for (int item : groupedItems.getOrDefault(
                    g, new ArrayList<>())) {
                result[index++] = item;
            }
        }

        return result;
    }

    private List<Integer> topoSort(
            List<List<Integer>> graph, int[] indegree) {

        Queue<Integer> queue = new LinkedList<>();
        List<Integer> order = new ArrayList<>();

        for (int i = 0; i < indegree.length; i++) {
            if (indegree[i] == 0) {
                queue.offer(i);
            }
        }

        while (!queue.isEmpty()) {
            int node = queue.poll();
            order.add(node);

            for (int next : graph.get(node)) {
                indegree[next]--;

                if (indegree[next] == 0) {
                    queue.offer(next);
                }
            }
        }

        return order;
    }
}
