class Solution {
    public int orangesRotting(int[][] grid) {
        int rows = grid.length;
        int cols = grid[0].length;
        java.util.Queue<int[]> queue = new java.util.LinkedList<>();

        int fresh = 0;
        int minutes = 0;

        // Add rotten oranges to the queue
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == 2) {
                    queue.offer(new int[]{i, j});
                } else if (grid[i][j] == 1) {
                    fresh++;
                }
            }
        }

        int[][] directions = {
            {-1, 0}, {1, 0}, {0, -1}, {0, 1}
        };

        while (!queue.isEmpty() && fresh > 0) {
            int size = queue.size();

            for (int i = 0; i < size; i++) {
                int[] orange = queue.poll();
                int r = orange[0];
                int c = orange[1];

                for (int[] d : directions) {
                    int nr = r + d[0];
                    int nc = c + d[1];

                    if (nr >= 0 && nr < rows &&
                        nc >= 0 && nc < cols &&
                        grid[nr][nc] == 1) {

                        grid[nr][nc] = 2;
                        fresh--;
                        queue.offer(new int[]{nr, nc});
                    }
                }
            }

            minutes++;
        }

        return fresh == 0 ? minutes : -1;
    }
}
