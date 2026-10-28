import java.util.*;

class Solution {
    public int[] shortestAlternatingPaths(
            int n, int[][] redEdges, int[][] blueEdges) {

        List<Integer>[] red = new ArrayList[n];
        List<Integer>[] blue = new ArrayList[n];

        for (int i = 0; i < n; i++) {
            red[i] = new ArrayList<>();
            blue[i] = new ArrayList<>();
        }

        for (int[] edge : redEdges) {
            red[edge[0]].add(edge[1]);
        }

        for (int[] edge : blueEdges) {
            blue[edge[0]].add(edge[1]);
        }

        int[][] dist = new int[n][2];
        for (int[] row : dist) {
            Arrays.fill(row, -1);
        }

        Queue<int[]> queue = new LinkedList<>();

        // Color 0 = red, color 1 = blue
        queue.offer(new int[]{0, 0});
        queue.offer(new int[]{0, 1});

        dist[0][0] = 0;
        dist[0][1] = 0;

        while (!queue.isEmpty()) {
            int[] current = queue.poll();
            int node = current[0];
            int color = current[1];

            List<Integer> nextNodes =
                (color == 0) ? blue[node] : red[node];

            int nextColor = 1 - color;

            for (int next : nextNodes) {
                if (dist[next][nextColor] == -1) {
                    dist[next][nextColor] =
                        dist[node][color] + 1;

                    queue.offer(new int[]{next, nextColor});
                }
            }
        }

        int[] answer = new int[n];

        for (int i = 0; i < n; i++) {
            if (dist[i][0] == -1) {
                answer[i] = dist[i][1];
            } else if (dist[i][1] == -1) {
                answer[i] = dist[i][0];
            } else {
                answer[i] = Math.min(dist[i][0], dist[i][1]);
            }
        }

        return answer;
    }
}
